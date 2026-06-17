# 毒舌产品经理V2.0 工作流

## 核心原则

毒舌产品经理V2.0 是一条用文档接力的 AI 产品生产线。

每个环节只做自己的事，产出一份可交接文档。下一个环节必须读取上游文档后再工作，不能只靠聊天上下文。

## 6 个主线环节

1. `Product Spec Builder`
   - 输入：用户的模糊想法
   - 输出：`artifacts/SPEC.md`
   - 目标：把想法逼问成可直接开发的需求文档

2. `Design Brief Builder`
   - 输入：`artifacts/SPEC.md`
   - 输出：`artifacts/BRIEF.md`
   - 目标：把感觉词变成明确的设计决策

3. `Design Maker`
   - 输入：`artifacts/SPEC.md`、`artifacts/BRIEF.md`
   - 输出：`artifacts/DESIGN.md`
   - 目标：生成视觉方案和高保真原型说明
   - 备注：可选环节

4. `Dev Planner`
   - 输入：`artifacts/SPEC.md`、`artifacts/BRIEF.md`、可选 `artifacts/DESIGN.md`
   - 输出：`artifacts/PLAN.md`
   - 目标：拆成可独立验收、每阶段都能跑起来看到效果的 Phase

5. `Dev Builder`
   - 输入：`artifacts/PLAN.md` 和上游全部文档
   - 输出：代码、`artifacts/BUILD_LOG.md`
   - 目标：按计划实现，每个任务完成后必须经过独立审核

6. `Release Builder`
   - 输入：代码、`artifacts/BUILD_LOG.md`、上游全部文档
   - 输出：`artifacts/RELEASE.md`
   - 目标：隐私审计、打包、发布、协助上传 GitHub

## 扩展环节

7. `Orchestrator`
   - 输出：`artifacts/RUN_STATE.md`
   - 目标：控制 agent 调度节奏，防止死循环、连续调用和 429

8. `Bug Fixer`
   - 输出：`artifacts/BUGFIX.md`

9. `Skill Maker`
   - 输出：新的 skill 文件夹

10. `Goal Writer`
   - 输出：`artifacts/GOAL.md`

11. `Evolution Steward`
    - 输出：`evolution/EVOLUTION_LOG.md`

12. `Independent Reviewer`
    - 输出：`artifacts/REVIEW.md`

## 串联规则

- 不允许跳过文档直接进入下游，除非用户明确要求临时试做。
- 下游发现上游文档不清楚，必须先补问题或回退到对应上游技能。
- 开发阶段每个任务必须形成有上限的闭环：实现 -> 独立审核 -> 最多 2 次修正/复审 -> 通过或交给 Orchestrator 暂停询问用户。
- 多 agent 工作流必须先经过 Orchestrator，限制单轮交接次数和重复修复次数。
- 同一任务审核失败两次后必须暂停并询问用户，不允许无限循环修复。
- 发布阶段必须确认不会把内部工作文件、隐私信息、密钥、聊天记录、开发者提示词或系统核心配置上传到公开仓库。
