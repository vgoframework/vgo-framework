# VGO Rank v1.0 — 证书签发、验证和撤销契约

状态：规范冻结；签发生产开关受 [服务架构 F08](RANK-SERVICE-ARCHITECTURE-V1.0.md) 约束。权威等级阈值见 [标准](VGO-RANK-STANDARD-V1.0.md)。

## 1. 证书主体和含义

只有 VGO Framework Issuer 能生成 `certificate_id` 和签名，Omseek/官网/伙伴仅持有引用。证书不表示产品质量或收入承诺；每一证书只对应一个实体、市场、语言、行业问题空间、观测窗口与 Rank 版本。`VR0` 是有效观测结果；`unrated/provisional/restricted/revoked/expired` 不可展示为当前认证等级。首发最高 VR8；开放 VR9/10 另需标准所列门槛。

JWS Compact Serialization，固定受支持算法 `ES256`，header `{alg:"ES256",kid:"<key-id>",typ:"vgo-rank+jwt"}`；签名输入为 base64url(header JSON UTF-8) + "." + base64url(payload JSON UTF-8)，ECDSA 签名为 64 字节 P-256 `R||S`。禁止 `none`、算法自动协商、从载荷指定远程 key URL。历史 JWK 在所有依赖该 key 的证书过期加 90 天内保持可检索。密钥于专用 KMS/HSM 内生成，issuer 仅有签名权限、无导出私钥权限；轮换产生新 kid，旧证书不重签。沙箱/生产使用不同 issuer、key、JWK、域名。

必需 payload：`iss`, `aud:"vgo-rank-verifiers"`, `jti`, `iat`, `nbf`, `exp`, `certificate_id`, `entity_id`, `entity_type`, `scope_id`, `market`, `locale`, `industry`, `question_space_version`, `surface_protocol_version`, `rank_protocol_version`, `window_start`, `window_end`, `level`（整数 0—10）, `s_raw`, `s_conservative`, `confidence_90:{lower,upper}`, `coverage:{planned,qualified,by_surface}`, `accuracy_gate`, `evidence_manifest_hash`, `score_run_id`, `roles:{standard_owner,evidence_providers,issuer,appeal_reviewer}`, `affiliations`。`exp-iat` 不超过 45 天，实际证书时间由月度签发确定；id 和 timestamp 格式在 OpenAPI 中固定。所有小数以整数基点（0—10000，代表百分比百分之一）序列化，消除浮点歧义，UI 自行格式化。证书载荷没有姓名、原始答案、保密题或客户 secret。

## 2. 状态是独立的权威事实

有效签名只证明签发时内容未被篡改，不证明当前仍有效。验证者必须：校验可信 issuer/HTTPS 主机与固定 aud、允许的 alg、kid 对应 JWK、签名、时间（时钟容忍 60 秒）、必需字段及 scope；再调用 `/v1/certificates/{id}/status` 读取与同一证书 ID 匹配、签名或可信传输、时间不超过 30 秒的当前状态。`rated` 和 `watch` 可显示等级（watch 须提示）；`restricted/revoked/expired/unknown` 或状态服务故障不能显示“有效认证”。证书到期按 exp 本地先行判无效。状态响应含 `certificate_id/status/effective_at/reason_code/status_version/checked_at/next_check_before`。历史原始 JWS 保留；撤销只追加状态事件，不能改写签名载荷。

官网徽章使用在线状态接口，仅在 rated/watch 时显示带当前 scope 的动态徽章；JS 加载失败回退到“暂无法验证”，不得使用静态有效图片。第三方可显示自己的 UI，但必须链接验证页且遵守商标许可。签发、状态变化、过期分别有 webhook，重复和乱序按证书 ID + 单调 `status_version` 消化。

## 3. 签发交易与审计

签发前服务检验 scope/版本、样本资格、分数闸门、校准报告和市场发布开关；签发操作者与复核者两名不同主体；待签 payload 哈希先封存，签名后原子保存 JWS、证据 manifest、状态事件和 outbox，失败不遗留可查询但无状态证书。证书 ID 唯一，针对同一 score_run 的重试幂等。签发日志记录签发者、审批人、代码/协议摘要、输入 evidence hash、关联披露与 request_id；调用方不可编辑。密钥滥用、重大事实纠错先 restricted，核实后 revoke/reissue 并说明替代证书；公开订阅状态更新，历史可追溯。

## 4. 必须通过的验证向量

正式发布前在仓库中固定可复算 fixture：有效签名；一个字节篡改；错误 aud/iss；不允许 alg；未知 kid；过期/未来 nbf；合法历史证书但现态 revoked/restricted；状态响应证书 ID 不一致；状态服务超时；签名后 payload 数值舍入；重复 webhook 和乱序 status_version；密钥轮换后旧证书。官网、Omseek、TS/Python SDK 用同一向量跑 CI；签名公钥和示例 JWS 只可由真实沙箱 key 生成，不在文档中伪造生产样本。
