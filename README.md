# 毒舌产品经理V2.0

毒舌产品经理V2.0 是一套用文档接力驱动的 AI 产品生产线。

它的核心不是让 AI 顺着用户夸，而是把模糊想法逼问、拆解、设计、计划、开发、审核、发布，最终变成可运行、可验收、可发布的产品。

## 如何使用

把本仓库放进要开发的项目文件夹后，让 Codex/GPT 先阅读：

```text
START_HERE_FOR_CODEX.md
```

推荐启动语：

```text
请先阅读 START_HERE_FOR_CODEX.md。这是毒舌产品经理V2.0 的操作手册。请作为 Orchestrator 编排器，按固定 agent 顺序推进，产出 artifacts 文档，不要把流程压缩成 1-2 个 agent。
```

这套系统不是普通代码模板，而是目标项目里的 agent 控制层：

- `START_HERE_FOR_CODEX.md`：入口说明书
- `agent/`：12 个 agent/skill
- `agent/workflow/COMMAND_POLICY.md`：命令、Git、依赖、发布操作的安全策略
- `artifacts/`：阶段交接文档
- `hooks/`：审核和发布门禁，包含 GitHub 发布和 Windows 安装包检查
- `evolution/`：自进化规则和记录

## 主线流程

1. 需求：`Product Spec Builder` -> `artifacts/SPEC.md`
2. 设计规范：`Design Brief Builder` -> `artifacts/BRIEF.md`
3. 设计图：`Design Maker` -> `artifacts/DESIGN.md`
4. 开发计划：`Dev Planner` -> `artifacts/PLAN.md`
5. 开发：`Dev Builder` -> 代码和 `artifacts/BUILD_LOG.md`
6. 发布：`Release Builder` -> `artifacts/RELEASE.md`

## 扩展角色

- `Orchestrator`
- `Bug Fixer`
- `Skill Maker`
- `Goal Writer`
- `Evolution Steward`
- `Independent Reviewer`

`Orchestrator` 是调度层，只负责控制 agent 运行节奏、防止死循环和 429，不负责写代码、设计、评审或需求。

## 命令与发布安全

任何终端命令、Git 操作、依赖安装、环境修改、删除操作、发布、部署或远程上传前，都必须先读取并应用：

```text
agent/workflow/COMMAND_POLICY.md
```

调用方法很简单：先判断命令风险等级，再决定能不能执行。只读命令可以自动执行；依赖、环境、Git 历史操作必须先获得用户明确确认；`git push`、强制推送、删除、发布、部署等远程或不可逆动作默认禁止，只有用户在当前会话明确确认具体命令、目标和目的后才允许继续。

发布或上传前，必须读取并应用：

```text
hooks/RELEASE_GATE.md
```

如果发布对象包含 `.exe`、`setup.exe`、`installer.exe`、Inno Setup `.iss` 生成的安装包或其他 Windows 可执行发布包，Release Builder 必须检查数字签名、SmartScreen reputation、Defender / antivirus 风险、安装包内容和隐私泄露风险。未签名安装包可以用于本地测试，但不能直接声称适合正式公开分发。

## 用户模式

系统区分两类用户：

- 会写代码的用户：可以接收命令、文件路径、diff、测试结果和技术取舍。
- 不会写代码的用户：只接收一步一个动作、产品影响说明、风险提示和 A/B/C 选项。

面向不会写代码的用户时，技术问题应转换成决策卡片：

```text
当前问题：登录按钮点击后没有反应。
技术原因：前端事件绑定缺失。
影响范围：首页登录区域。
推荐方案：只修改 LoginButton 组件，不动后端。
风险：低。
是否允许继续修改？
```

非技术用户不需要参与库选择、文件结构、实现模式等低层技术细节；只有高风险、范围变更、成本增加、发布、账号权限、数据暴露或不可逆动作时才需要用户确认。

## 关键目录

- `agent/skills/`：12 个专门技能
- `agent/workflow/`：工作流、文档契约、产物规则和命令安全策略
- `artifacts/`：各环节交接文档
- `evolution/`：自进化规则和日志
- `hooks/`：审核门禁和发布门禁

## 核心原则

- 靠文档串联，不靠聊天上下文续命。
- 每个环节只做自己的职责。
- 多 agent 工作流先由 Orchestrator 控制节奏，避免死循环和 429。
- 执行命令前先应用 `COMMAND_POLICY.md`，不要静默执行高风险命令。
- 面向不会写代码的用户时，一次只给一个安全动作，不把终端、Git、部署错误丢给用户自己判断。
- 开发任务必须经过独立审核。
- 发布前必须做隐私审计，并按 `RELEASE_GATE.md` 检查发布风险。
- 仓库署名属于用户，不默认写 GPT 或 Codex。
- 提交 GitHub 前必须确认目标仓库是否是用户指定仓库。
