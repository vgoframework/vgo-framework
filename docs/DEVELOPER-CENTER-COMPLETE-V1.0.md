# VGO Framework 开发者中心与开放平台完整方案 v1.0

**决策状态：开发契约冻结；开放状态由实际部署和验收决定。** 日期：2026-09-29。标准权威：[VGO Rank v1.0](VGO-RANK-STANDARD-V1.0.md)；HTTP 权威：[OpenAPI 3.1.1](rank-openapi-v1.0.yaml)；签发与验证：[证书规范](RANK-CERTIFICATE-AND-TRUST-V1.0.md)；服务：[架构与任务](RANK-SERVICE-ARCHITECTURE-V1.0.md)。本文件是开发者中心的产品、信息架构、接入和发布完整契约。Omseek 开放平台另属 Omseek：它提供客户工作流和治理执行，而 Framework 提供公用标准、正式评测和可验证证书。

## 1. 用户与产品边界

开发者中心服务五类人：①引用标准的研究者与企业；②验证证书的采购方、媒体和机器客户端；③嵌入动态徽章/榜单的站点；④经授权发起诊断/评级的 SaaS、代理和 Omseek；⑤审核数据与方法的独立评估者。开发者不必购买 Omseek 才能阅读标准、核验证书或提交基本纠错。Omseek 是发起者与首个产品接入方，关联关系、共享人员和四种证书角色公开披露。开发者中心不展示保密正式题库、私有证据、运营签发开关、客户跨租户数据或 KMS 控制。

能力层级与页面显示状态分别定义，避免“API 已开放”一语概括：

| 层级 | 能力 | 凭证 | 上线策略 |
|---|---|---|---|
| L0 | 标准、方法、版本、状态、概念、OpenAPI 文件 | 公开 | 标准页可先发布 |
| L1 | 证书/现态、验签、已批准榜单与动态徽章 | 匿名或只读身份 | Framework 正式签发与法务发布门槛通过后开放真实数据 |
| L2 | 隔离沙箱、模拟任务与样本证书 | 沙箱 client/key | 沙箱、向量和安全测试通过后开放，显著标明不能作为正式评级 |
| L3 | 经授权的实体、作用域、诊断、行动/复测 | OAuth2 + 客户授权 | 审核主体分批接入，私有证据受最小权限保护 |
| L4 | 正式评级申请、事件订阅、伙伴规模集成 | OAuth2 + 资格/配额 | 评级服务和治理门槛通过后分批开放；付费不改变正式资格和采样 |
| L5 | 题库封存、算分、审核、签发、撤销、申诉裁决 | Framework 内部隔离身份 | 永不作为公共门户操作面 |

每项页面、操作和 SDK 方法展示 `planned/sandbox/limited/production/deprecated`、最后更新、API 版本、协议版本及环境链接；planned 不显示可点击生产调用。门户文案中“标准冻结”与“生产开放”是不同状态。L0 首发不依赖 L1–L4 运行；L1 未开放时不得发布真徽章或伪榜单。

## 2. 页面与导航（英根路径、中文 /zh）

- `/developers`：能力矩阵、三条接入路径、各级状态、关联披露、状态页和升级日志。
- `/developers/api`：OpenAPI 下载、主机/环境、鉴权、资源图、逐 operation reference、分页、异步任务、错误码、429、版本和弃用。
- `/developers/sdk`：已发行 TS/Python 包的真实安装指令、兼容表、源代码、签名验证、最小可运行示例；未发行显示计划而不放假命令。
- `/developers/quickstart`：公开核验；沙箱诊断；正式申请三条分开的可运行教程。生产教程只在真实环境通过 CI 后可见。
- `/developers/webhooks`：订阅、HMAC 原文字节验签、重试/去重、乱序与死信、秘钥轮换及测试事件。
- `/developers/changelog`：API/Rank 协议/SDK 三条独立版本轴，兼容和迁移窗口。
- `/developers/status`：各环境能力可用性、事故与历史，不代替证书的权威现态。
- `/rank`、`/rank/methodology`、`/rank/certificates/{id}`、`/governance/appeals`：解释、验证、纠错；正式查询可由公开 API 支撑，不要求登录 Omseek。

现有官网保留 `/developers`、`/developers/api`、`/developers/sdk` 等预留路径。新路径与 CMS 旧址、保留词、canonical、hreflang、sitemap 一起审查；内容从 Framework 固定 commit 导入，网站不得编辑同一标准版本的阈值。OAuth 凭证、证书私钥、签发职能不放在官网 CMS。

## 3. 资源、协议与 OpenAPI

HTTP 基地址规划为 `https://api.vgoframework.org/v1`，沙箱 `https://sandbox-api.vgoframework.org/v1`；均在域名真实部署后才公开为可用。OpenAPI 3.1.1 的单一源文件为 `docs/rank-openapi-v1.0.yaml`；网站从固定 Framework commit/hash 导入，禁止维护分叉的 API schema。资源包含 protocols、entities、scopes、diagnostic-runs、rating-requests、certificates/current/status/verify、rankings、appeals、subscriptions 和 JWK；动作与响应详见契约。公开证书验证只接受证书 ID 或 JWS，不对用户 URL 发起抓取。榜单只含合格公开列名实体、同市场同语言同问题空间同协议，默认 20、最多 100、游标分页；样本队列不足 30 不显示分位。

`GET /certificates/{id}` 返回历史签发 JWS；`GET /certificates/{id}/status` 是当前状态；`POST /certificates/verify` 组合签名/时间/作用域/现态验证；`GET /rankings` 是受发布开关控制的公开榜单。请求评级返回 202 job ID，`completed` 不等于 `certificate.issued`。无评级返回明确 `unrated` 原因，VR0 仅代表合格观测后的 0 级。所有当前有效展示同时检查原始签名和不超过 30 秒的现态；传播限制/撤销到官网、API、动态徽章上限 60 秒。历史 JWS 不回写。

OpenAPI 必须经过语法、引用、schema、operationId 唯一、auth scope、错误、样例、运行 HTTP 一致性验证；CI 对 breaking diff 阻断。只有符合生产契约测试的 operation 可标 production。OpenAPI 主版本 `/v1` 与 Rank 评分协议 `1.0` 各自版本化；破坏性 API 变更走 `/v2` 和至少 90 天公告/迁移，安全紧急关停例外并公开原因。证书 `rank_protocol_version` 永远保留签发时版本。

## 4. 身份、授权、配额与账单边界

L1 公开 GET 匿名，验证 POST 匿名受限流；L2 沙箱 client/key 一次显示、存摘要、30 天到期，环境完全隔离；L3/L4 OAuth2 client credentials，10 分钟 token、Framework audience、最小 scope，客户实体授权单独核实。初始 L1 匿名每来源 IP 每分钟 60 GET、10 verify POST；L2 每 key 每分钟 60、每天 1000、真实诊断预览每天 3、并发 1；L3/L4 内测每 tenant 每天 20 个计算任务、并发 2。这些是运维限额，不是分数权重；实际发布配置须显式公开并可运维审批调整。429 携 Retry-After、限制/剩余/重置。扩大额度不改变正式抽样和等级。

资格、免费纠错和正式抽样不与付费绑定。更深私有诊断可单独订价，但首期不建设公开自动扣费或“买正式等级”流程。伙伴授权由各自组织和客户授予，Omseek 不能给其他伙伴签发 Framework 证书；浏览器不能保管服务端 secret。跨租户身份、scope、证据读权限和访问日志须回归测试，删除/导出请求按适用政策处理。

## 5. 证书、事件、纠错

证书 JWS Compact ES256，使用受信 issuer/aud/kid，P-256 托管 KMS/HSM 不可导出；生产/沙箱分离。官网/SDK 验原始字节签名，不重序列化 payload；再向权威状态查询，超时/未知/限制/撤销/过期一律不显示有效徽章。生产活动签发 key 每 90 天轮换，新公钥提前 7 天公布；旧公钥支持历史校验，泄露时停用签发并公开 key 状态及涉案证书复核。签发权授予与生产 key 激活须两人批准，关联案件回避。

事件订阅是至少一次送达，采用独立 **HMAC-SHA256** secret 对 `timestamp + "." + raw_body` 签名，头部 `X-VGO-Signature` 为小写 hex；5 分钟容忍；重试保留 event_id 可更新 timestamp，最长 24 小时并进入死信，接收端先持久化后应答，`status_version` 防乱序。这里明确以已冻结 Framework 签发/开发者契约为准；旧官网 D08 的“Webhook ES256 JWS 信封”仅作历史设计，不用于 v1.0。证书 ES256 与 Webhook HMAC 不能混淆。

任何人可免费提交基本事实纠错，不以客户认领为条件。按 Rank v1.0：3 工作日确认，明显身份/事实错误 5 工作日先行限制与核查；一般 15 工作日附理由答复，复杂案告知延期且总计最多 30 工作日。旧官网 D14 的 2/20+20 时限被本版替代。争议由无关联复核人处理；有证据的撤销、重签和理由进入公开状态历史，不能静默改级。涉及隐私的证据不公开。

## 6. SDK、沙箱与测试

SDK 分层发布：OpenAPI/sandbox/签名向量与运行契约通过后优先 TypeScript，再 Python；v1 首批对外暴露只读核验方法，L3/L4 在各自接口验收后扩展。SDK 的 `verifyCurrent` 必须返回签名结果、现态、查询时间及 reason，而非布尔真值；不能只靠本地 JWS 判断 current。HTTP 层包含超时、取消、重试、幂等 key、结构化错误、request ID、scope 和环境隔离。每个 SDK 发布包绑定 OpenAPI SHA 和支持的 API/Rank 版本。

沙箱拥有独立 issuer/JWK/凭证、隔离实体和示例证书；不可把沙箱 VR 当正式等级，也不可访问生产客户。测试向量至少覆盖有效、篡改、未知 kid、错误 issuer/aud、过期、VR0、unrated、watch、restricted、revoked、状态超时、密钥轮换、同名/无网站、故障样本、重复/乱序 webhook、idempotency 冲突和申诉。新示例只在 CI 对真实沙箱运行成功后放在 quickstart。

## 7. 发布阶段、验收与运营

| 阶段 | 可发布内容 | 不可声称 | 验收 |
|---|---|---|---|
| A 标准门户 | 双语标准、契约、状态 planned、治理/纠错说明 | 生产 API/证书/榜单已开放 | 内容 hash 与标准版本一致、旧址及无假按钮验证 |
| B 沙箱 | L2、测试向量、TS SDK 只读核验 | 沙箱为正式评级 | 沙箱和生产隔离、端到端 quickstart、速率/权限测试 |
| C 正式只读 | 证书、现态、验证、已批准榜单 | 所有私有接口普遍开放 | Framework F08、法务、证书撤销 60 秒、官网/SDK 联测 |
| D 授权扩展 | L3/L4 经审核主体和逐项授权 | Omseek 客户优待或付费提级 | 合约、隔离、申诉、配额、计费与合作伙伴用例验收 |

发布审计逐项记录：Framework 服务版本、OpenAPI SHA、市场协议/校准报告、真实运营主体和利益关联、KMS/JWK/轮换、撤销演练、法律审查、网站内容 hash、SDK 版本、示例运行日志和回滚方案。缺一项则只关闭相应能力，不将 planned 偷换 production。运营后台显示入口与任务状态、证据质量、签发双人审批、申诉 SLA、事件死信、密钥状态、API 速率和错误趋势；它是 L5 内部工具，不作为公共开发者门户。

## 8. 与既有官网 D04–D16 决策的取舍

| 旧决策 | v1.0 裁定 |
|---|---|
| D04 数值须实测后确定 | 2026-09-29 冻结标准给定 v1.0 规范阈值；实测是正式签发准入，不以观测资料追溯私改阈值。验收失败发布新协议版本。 |
| D06 OpenAPI 3.1.1、`api/openapi.yaml`、验证/榜单、错误 envelope | 保留 3.1.1、验证和榜单；单源文件现为 `docs/rank-openapi-v1.0.yaml`，官网从此导入。v1 HTTP envelope 以该文件为准，旧草案 envelope 不作为并行实现。 |
| D07 JWS ES256、KMS、90 天轮换 | 保留并补入本规范；签发内容以冻结证书契约为准。 |
| D08 Webhook ES256 | v1 改为独立 HMAC-SHA256；证书 ES256 不变，官网接收器按 HMAC 更新。30 秒状态新鲜度、60 秒传播门槛保留。 |
| D09 权限与初始运维配额 | 保留层级、10 分钟 token 与额度；将 OpenAPI scopes 与门户层级映射。 |
| D14 2/20+20 工作日 | 改按 Rank v1.0 的 3/15/30 工作日、明显错误 5 日先行限制。 |
| D16 TS→Python、真实沙箱后 SDK | 保留；先只读核验，后授权诊断/评级。 |

此表是跨仓库变更决策记录。官网仓库的历史 D 文件保留以追溯，但须加“由本版取代的条款”链接；未列出的旧部署、备份、双语、旧址和 CMS 规则保持有效。
