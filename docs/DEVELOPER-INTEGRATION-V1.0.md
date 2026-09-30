# VGO Framework v1.0 — 开发者接入与发布契约

**文档状态：接口规范已冻结，沙箱/生产端点和 SDK 尚待实现与联调。** 以 [OpenAPI](rank-openapi-v1.0.yaml) 为 wire schema，以 [评级标准](VGO-RANK-STANDARD-V1.0.md) 和 [证书规范](RANK-CERTIFICATE-AND-TRUST-V1.0.md) 为语义及信任依据。示例 URL 是规划域名，不是现已可访问服务；不得展示虚构的成功响应。

## 接入模式

| 模式 | 能力 | 凭证与边界 |
|---|---|---|
| 公开核验 | 协议列表、证书、状态、JWK | 匿名 HTTPS；速率限制；实时状态，绝不代签 |
| 授权诊断 | 提交实体/作用域，运行诊断、阅读授权摘要 | OAuth2 client credentials + 客户授权；不含正式证书 |
| 正式评级申请 | 申请评测、轮询结果、接收事件 | `ratings:request`，资格与正式题库由 Framework 控制；申请不能指定分数 |
| 伙伴应用 | 上述能力 + 回调订阅、授权证据读取 | 独立 client_id、环境、tenant、scope、预算；不得转交凭证 |
| Omseek | 与伙伴相同正式评级调用面；可叠加自有商业优化流程 | 关联关系显著披露；无内部签发捷径 |

接入顺序：申请沙箱 client → 确认客户授权和 entity → scope → 诊断 → （可选）正式评级申请 → 异步任务结果 → 获取 JWS → 本地验签 + 查询当前状态 → 展示带作用域和有效期的等级 → 订阅更新/免费申诉。未评级、provisional、未通过发布门槛时不能输出认证徽章。正式请求可返回 `insufficient_evidence`，不能当 VR0。品牌与产品、城市与全国分别申请 scope。

`Authorization: Bearer <token>` 在服务端发送，`Idempotency-Key` 对同一请求重试保持不变。读取证书可匿名，读取私有诊断需授权。429 按 Retry-After，5xx 指数退避，409 不自动换 key 重试；异步回调可重复和乱序，先用 `event_id` 去重，再比较 `status_version`，展示前始终查当前状态。公网回调必须 HTTPS、验证 timestamp + HMAC-SHA256(raw request bytes) 的 `X-VGO-Signature`，容忍窗口 5 分钟，secret 轮换双密钥重叠最长 24 小时；规范化消息为 `timestamp + "." + raw_body`，头值为小写十六进制摘要。证书签名 ES256 与 webhook HMAC 用途不同，不共享 key。

## 错误、分页和限制

错误 envelope 为 `request_id/code/message/retryable/details`；HTTP 400/401/403/404/409/422/429/5xx 与稳定错误码见 OpenAPI。公开列表采用 opaque cursor，稳定排序，客户端不得从 cursor 推导信息；限制由环境公开配置发布，不在未上线前伪称具体 QPS。服务终止/协议退休提前公告及迁移期；签发的旧证书保留原协议和历史状态。每次正式请求记审计、授权及关联主体，不因为购买 Omseek 优先采样。

## SDK 交付清单

TypeScript `@vgoframework/rank`、Python `vgo-rank` 只从冻结的 OpenAPI 生成基础类型，再手写安全 verifier、任务等待器、分页、幂等和 webhook 验证器。两者必须暴露 baseURL、timeout、abort/cancel、持久化 idempotency key、结构化错误和证书当前态验证；默认拒绝未知 enum、错误 issuer、签名失败、过期与状态服务不可用。生成物标记 OpenAPI SHA-256 和协议兼容范围。发布前 CI 在同一沙箱 fixture 上覆盖品牌/产品、无网站、样本不足、VR0、签发、watch、restricted、revoked、密钥轮换、重复事件与申诉。

官网 `/developers/api` 公布 API 版本、状态（planned/sandbox/public）、OpenAPI 下载及运行样例；`/developers/sdk` 仅在 SDK 真正发布后展示可执行安装命令。正式证书徽章与商标使用须遵守单独的商标许可，公开标准 CC BY 不自动授予认证标志使用权。法律/数据处理协议、OAuth client 申请入口、支持和版本公告在生产开放前补齐实值并测试，不得放占位链接。


## Diagnosis v1 contract alignment (2026-10-01)
Authorized Diagnosis uses `docs/diagnosis-openapi-v1.0.yaml` for run/result operations and `docs/VGO-DIAGNOSIS-IMPLEMENTATION-SPEC-V1.0.md` for runtime semantics. Integrators use `diagnostics:run` for create/cancel/verification and `diagnostics:read` for private results; `evidence:read` is separately authorized. Shared entity/scope creation remains defined by the Rank/shared OpenAPI. Diagnosis webhooks use the same HMAC-SHA256 delivery platform and event_id dedupe rules; Diagnosis event envelope uses `type/created_at/aggregate_id`, while legacy Rank event payload retains `event_type/occurred_at/resource_id/status_version`. SDKs MUST model these as versioned event unions rather than assuming identical payload fields.
