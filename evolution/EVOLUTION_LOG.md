# Evolution Log

## 2026-06-13

- 初始化毒舌产品经理V2.0 的文档接力工作流。
- 定义 6 个主线环节和 5 个扩展角色。
- 约定通过 `artifacts/` 中的交接文档维持上下文连续性。

## 2026-06-16

- 触发原因：用户反馈在其他项目使用时，外部 Codex 最多只调用了 1-2 个 agent，且没有触发自进化。
- 观察到的问题：`START_HERE_FOR_CODEX.md` 对编排责任、固定顺序、强制交接和自进化检查写得不够硬，容易被理解成按需挑选单个 skill。
- 修改内容：强化入口文件，新增 Active Modes、Canonical Agent Order、Mandatory Handoffs、Self-Evolution Check，并明确 Full Pipeline Mode 不允许压缩成 1-2 个 agent。
- 影响范围：其他 Codex/GPT 接手本仓库时，应先作为编排器按固定顺序推进，而不是直接进入开发或只调用少量 agent。
- 回滚方式：还原 `START_HERE_FOR_CODEX.md` 到提交 `7fcb978` 的版本，并移除此条进化记录。

## 2026-06-16

- 触发原因：用户明确了目标使用方式：把毒舌产品经理V2.0 放进要开发的项目文件夹，再让其他 GPT 阅读入口文件并进入自动化流程。
- 观察到的问题：入口文件缺少“嵌入到目标项目后如何定位自身、如何区分控制系统与目标项目、如何自动编排”的说明。
- 修改内容：在 `START_HERE_FOR_CODEX.md` 新增 Deployment Model 和面向其他 Codex/GPT 的 Bootstrap 示例提示词。
- 影响范围：外部项目中的 Codex 应把本系统视作编排控制层，把目标项目视作产品工作区，并主动按固定顺序推进。
- 回滚方式：删除 `START_HERE_FOR_CODEX.md` 中 Deployment Model 与 Bootstrap 示例，并移除此条进化记录。

## 2026-06-16

- 触发原因：用户要求提交 GitHub 前必须确认目标仓库是否是用户指定仓库。
- 观察到的问题：原发布流程只要求上传前询问，但没有强制核对当前 remote 是否匹配用户指定仓库。
- 修改内容：更新 `release-builder`、`RELEASE_GATE.md`、`START_HERE_FOR_CODEX.md` 和 `artifacts/RELEASE.md`，要求 push 前展示目标仓库并获得用户确认；仓库缺失或不清楚时必须让用户提供仓库名称或 URL。
- 影响范围：所有 GitHub 上传流程在远程 push 前增加仓库确认门禁，避免误提交到错误仓库。
- 回滚方式：移除上述文件中的仓库确认要求，并删除此条进化记录。

## 2026-06-16

- 触发原因：用户反馈多 agent 连续运行容易触发 429，并担心进入死循环无限烧 token。
- 观察到的问题：原流程要求 Dev Builder 和 Independent Reviewer 闭环，但没有设置调度层、交接上限、失败上限或 rate-limit 停止条件；`fix and repeat until review passes` 存在无限循环风险。
- 修改内容：新增 `orchestrator` 调度层 skill，增加 `artifacts/RUN_STATE.md` 契约，更新入口文件、主流程、开发/审核 skill，限制单轮交接、重复修复和 429 风险。
- 影响范围：多 agent 工作流必须先经过 Orchestrator 控制节奏；同一任务审核失败两次后暂停询问用户；遇到 429 或额度压力时停止而不是继续派生 agent。
- 回滚方式：删除 `agent/skills/orchestrator`，移除 `RUN_STATE.md` 契约和各文件中的调度层限制，并删除此条进化记录。

## 2026-06-16

- 触发原因：用户指出系统面对会写代码和不会写代码的用户时风险完全不同，不懂代码的用户可能被 Git、终端、部署和报错流程困住。
- 观察到的问题：入口和发布流程没有先判断用户技术水平，也没有为非技术用户设置“一次一个安全动作”的交互规则。
- 修改内容：新增 Technical User Mode 与 Non-Technical User Mode，要求 Orchestrator 识别用户能力；非技术用户默认一步一步引导，不让用户独自解释终端、Git、部署或 stack trace 错误。
- 影响范围：GitHub 上传、环境设置、部署、报错处理和外部手动操作都必须按用户能力分层输出。
- 回滚方式：移除 `START_HERE_FOR_CODEX.md`、`orchestrator`、`release-builder`、`README.md` 与 `RUN_STATE.md` 契约中的用户能力分层规则，并删除此条进化记录。

## 2026-06-16

- 触发原因：用户建议把技术问题转换成“问题 / 原因 / 影响 / 方案 / 风险 / 是否继续”的决策卡片，帮助不会代码的人做判断。
- 观察到的问题：虽然已有 Non-Technical User Mode，但还没有统一的技术问题可视化格式。
- 修改内容：在 `Orchestrator`、`START_HERE_FOR_CODEX.md` 和 `Release Builder` 中加入决策卡片格式，要求把技术问题先翻译成可读决策，再请求用户确认。
- 影响范围：所有技术报错、Git/GitHub 问题、部署问题和执行风险现在都能用统一卡片形式呈现给非技术用户。
- 回滚方式：移除上述文件中的决策卡片格式，并删除此条进化记录。

## 2026-06-16

- 触发原因：用户进一步提出，非技术用户不应该参与技术细节，而应只看到产品影响、A/B/C 选择和关键风险确认。
- 观察到的问题：决策卡片仍可能让非技术用户参与过多技术细节，没有明确“什么时候才需要问用户”。
- 修改内容：更新 `Orchestrator`、`START_HERE_FOR_CODEX.md` 和 `Release Builder`，要求把技术问题翻译成产品影响，把复杂决策压缩成 A/B/C，并且只在高风险、范围变更、成本增加、发布、账号、数据暴露或不可逆动作时询问用户。
- 影响范围：非技术用户默认不参与库选择、文件结构、实现模式等低层技术决策；系统应选择最低风险的小范围修复并用产品语言总结。
- 回滚方式：移除上述文件中的 A/B/C 决策和关键风险询问规则，并删除此条进化记录。

## 2026-06-16

- 触发原因：用户发现公开发布文档中暴露了个人 Git 身份信息。
- 观察到的问题：`artifacts/RELEASE.md` 记录了具体账号和邮箱，公开仓库不应保存这类可识别身份信息。
- 修改内容：移除公开 release 文档中的个人账号和邮箱，更新 Release Builder、Release Gate、入口文件和隐私排除清单，禁止公开文档写入用户邮箱、账号、具体仓库 URL 等身份信息。
- 影响范围：后续发布文档只能使用通用表述，例如“使用用户自己的本地 Git 身份”，并建议使用 GitHub no-reply 隐私邮箱。
- 回滚方式：不建议回滚；如必须回滚，需先确认不会重新暴露个人信息。

## 2026-06-18

- 触发原因：Windows 安装包在开发测试中被系统安全机制拦截，关闭 Smart App Control 后可以运行。
- 观察到的问题：原 Windows 发布检查只覆盖 SmartScreen、Defender 和未签名安装包风险，没有明确 Smart App Control、Mark-of-the-Web、发布者信息、版本信息和 `.iss` 元数据诊断顺序；Bug Fixer 也可能把安全信誉拦截误判为应用代码错误。
- 修改内容：更新 Release Gate、Release Builder、Bug Fixer、入口文件、README、RELEASE 文档契约和 release artifact，新增 `docs/windows-install-troubleshooting.md`，要求先区分 Windows 安全信誉、签名、打包配置和真实运行时 bug。
- 影响范围：目标项目发布 Windows `.exe`、installer 或 Inno Setup 安装包时，必须检查 Smart App Control / SmartScreen / Defender 风险、签名、发布者和版本信息、SHA256、可信分发渠道；不得把关闭 Windows 安全功能作为正式发布方案。
- 回滚方式：移除上述文件中的 Windows 安装包安全诊断规则，并删除 `docs/windows-install-troubleshooting.md`；不建议回滚，除非后续有更完整的 Windows 发布策略替代。
