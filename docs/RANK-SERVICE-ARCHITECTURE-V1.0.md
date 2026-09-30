# VGO Rank v1.0 — 服务架构、能力边界与交付验收

状态：**实施契约冻结，未声明服务已上线**。规范依据：[Rank v1.0 标准](VGO-RANK-STANDARD-V1.0.md)。公开 HTTP wire contract：[OpenAPI](rank-openapi-v1.0.yaml)。证书：[签发规范](RANK-CERTIFICATE-AND-TRUST-V1.0.md)。任何数值或状态语义冲突，以标准为准；接口字段和路径以 OpenAPI 为准；签名字节格式以证书规范为准。

## 一、权限和部署边界

| 能力 | Framework 服务 | Omseek | 外部开发者 | 官网 |
|---|---|---|---|---|
| 实体消歧、作用域、正式题库和市场协议 | 主控、版本化 | 提交候选及授权事实 | 提交候选及授权事实 | 阅读公开版本 |
| 正式采样、证据账本、判定、评分 | 主控、封存题库、审计 | 可供给带来源的观测候选，不得改正式账本 | 同等条件供给候选 | 只读摘要 |
| 诊断、VHI、行动与复测 | 定义公共语义和授权接口；可委托执行 | 客户流程、资产和动作执行 | 自建优化器或调用授权诊断 | 展示解释 |
| 正式签发、限制、撤销、申诉裁决 | 唯一权威，独立权限、密钥和日志 | 只读、转发与显示 | 只读、验证与申诉 | 实时校验状态 |
| 私有客户数据、计费、代理、Studio | 不接管 | 主控 | 各自实现 | 不接管 |

同一团队或基础设施可以开发与部署，但 production 凭证、数据库写权限、密钥、签发角色与审计日志必须隔离。Framework 服务不能通过 Omseek 客户数据库直接签发；Omseek 不得伪造 Framework 的公开主机或镜像签名状态。主体运营关联和四种证书角色公开披露。首发可共享人员，不宣称组织独立。

## 二、服务组成与数据谱系

1. `EntityRegistry`：稳定 entity ID、品牌/产品类型、别名、市场与身份验证，合并和更名保留映射及历史；每次申请生成 `scope_id`。
2. `ProtocolRegistry`：Rank、问题空间、观测面和判定规范版本，正式题库封存，发布公开 manifest 与哈希。客户端不可列出保密题目。
3. `ObservationScheduler`：按市场协议生成计划、入口、随机种子与重试；区分 provider 失败、拒答、实体缺席。租户不可指定正式采样答案或次数。
4. `EvidenceLedger`：保存不可变原文、抓取时间、入口、区域/语言、解析版本、授权和内容哈希；敏感原文受控保留，删除请求与审计保全分离。
5. `Adjudicator`：P/U/C/R、NA、严重错误、付费位置、同源互证；10% 抽检和争议双人复核，判定/推翻均追加事件。
6. `RankCalculator`：按协议确定性合成、2,000 次题目聚类 bootstrap、闸门、等级状态与上下限。产物锁定输入证据集和代码/协议摘要，可同一快照复算。
7. `Issuer`：仅在发布门槛通过、当前市场协议有效、四眼审批、密钥有效时签发；写不可变 payload、签名、状态事件及审计事件，并通过 outbox 发布。
8. `Appeals`：免费受理，自动关联涉案证据、回避签发参与者、留理由与时限；必要时限制、撤销及重签。
9. `PublicRegistry`：公开证书、当前状态、JWK、市场协议、订阅事件、纠错入口；默认关闭未经审核的个人实体公开列名。

数据库的 `entity / scope / protocol / question_set / sample_plan / observation / evidence / adjudication / score_run / certificate / status_event / appeal / audit_event / outbox` 分别有不可变 ID、created_at、actor、correlation_id 和版本。正式证据和签发记录 append-only；撤销追加事件，不更新原始事实。授权数据的保留期限与删除请求由适用法律及协议确定，公开证书只含最小字段。

## 三、操作边界与流转

`POST /v1/entities` 和 `/v1/scopes` 是候选实体/作用域申请，不保证资格；诊断通过授权 scope 获取运行与证据摘要。正式评级申请 `POST /v1/rating-requests` 返回 202 和 job ID；Framework 自行选择封存题库和计划，客户端不得上传最终分数。`GET /v1/rating-requests/{id}` 可见 queued/running/insufficient_evidence/completed/failed 及门槛原因。完成并不等于签发；只在 issuer 审核通过后生成证书。公开 `GET /v1/certificates/{id}` 与 `/status`、`/.well-known/jwks.json` 可匿名调用，受速率限制；`GET /v1/scopes/{id}/current-certificate` 不存在时返回明确无现行证书，不给 VR0。`POST /v1/appeals` 免费，未认领第三方可提交并经身份/影响验证。

Webhooks 采用 at-least-once，事件 ID 去重、签名、时间窗和重放防护；无法投递进入死信与受权重放。`rating.completed` 不代表 `certificate.issued`。撤销和过期状态以同步权威查询为准，webhook 仅加速缓存失效。公开查询缓存 active 状态不超过 30 秒，失败时 fail closed；证书历史仍可读取。

## 四、鉴权、版本与错误

生产授权使用 OAuth2 client credentials（服务端到服务端）。共享 scope 注册表为 `entities:write / diagnostics:run / diagnostics:read / evidence:read / protocols:read / ratings:request / appeals:write / subscriptions:write`；公开读取匿名。凭证按 partner、environment、subject 和最大作用域约束；Omseek 与外部开发者同一 contract，不共享客户 secret。用户代表访问须附客户授权、tenant 映射与过期撤销；前端不持有客户端密钥。申请、申诉和订阅写入使用 `Idempotency-Key`（有效 24 小时），相同 key 不同 body 返回 409；响应含 `request_id` 和稳定错误 `code/message/details/retryable`。429 附 Retry-After，5xx 可安全重试，所有分页稳定 cursor。

`/v1` 主版本稳定；新增可选字段为兼容变更，删除/重释字段或收紧输入须 `/v2`、迁移窗、契约差异报告。Rank 协议版本与 HTTP 版本相互独立。服务不满足外部接入准备时不发布 SDK 为“可用”。原始证据访问默认私有；公开摘要保留证据类型、数量、覆盖和哈希，不泄露保密题库、个人数据或无授权版权内容。

## 五、落地任务和验收

| ID | 交付 | 完成证据 |
|---|---|---|
| F01 | 仓库新增独立评级服务、独立 DB schema、迁移、角色与签名密钥配置 | Omseek 凭证无法写正式证书或密钥；审计查询可验证 |
| F02 | 实体/作用域注册、消歧和市场协议 manifest | 更名、同名、无网站、跨市场用例；版本哈希可核对 |
| F03 | 题库、调度、真实入口采样和故障分类 | 120 题、分层比例、三批次、至少 720 合格机会等门槛在运行报告可复现 |
| F04 | 证据账本、四态判定、双人复核和抽检 | 付费位置排除、错误事实和 NA 场景、10% 抽检有记录 |
| F05 | 算分、置信区间、闸门、升降级 | 固定输入/种子重复产出相同结果；边界值、首次评级及版本断点回归 |
| F06 | 签发、密钥轮换、状态、撤销及申诉 | 签名测试向量、篡改拒绝、状态机、15/30 天时限和角色回避 |
| F07 | OpenAPI、授权、webhook、SDK 与 sandbox | CI 校验 schema/运行路由/SDK 差异；外部伙伴沙箱独立完成请求、核验和订阅 |
| F08 | 首发准入 | 两轮 30 天实测、30 实体、质量/法律/关联披露/撤销演练、校准报告全通过后才开签发开关 |

首发前公开 swagger 文档、错误码、沙箱主机、测试凭证领取、速率限制、数据与版权政策、服务状态、变更日志、支持与申诉联系点。各任务可编码并跑 CI，但 F08 未通过时签发密钥的 production 使用能力保持关闭；正式徽章和榜单不得出现。不得把 V1.0 文档当作既有服务能力。
