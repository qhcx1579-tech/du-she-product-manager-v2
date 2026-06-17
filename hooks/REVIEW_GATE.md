# 审核门禁

## 触发时机

Dev Builder 每完成一个任务或一个 Phase，必须触发 Independent Reviewer。

## 通过条件

- 功能符合 `SPEC.md`
- 视觉和交互不违背 `BRIEF.md`
- 代码和实现不偏离 `PLAN.md`
- 可运行、可验收、可复现
- 没有明显隐私泄漏或密钥泄漏

## 不通过处理

审核不通过时，Dev Builder 可以修复问题并再次请求审核，但同一任务最多允许 2 次修复/复审循环。

如果第 2 次复审仍不通过，必须停止自动修复，交给 Orchestrator：

- 记录失败原因到 `artifacts/RUN_STATE.md`
- 总结重复问题和当前安全状态
- 向用户询问是否继续、缩小范围、回退方案或调整需求

只有审核通过后，该任务才算完成。

禁止开放式循环：

- 不允许无限重复 `Dev Builder -> Independent Reviewer`
- 不允许为了“再试一次”继续消耗 token
- 遇到 429、额度压力或重复问题时必须暂停
