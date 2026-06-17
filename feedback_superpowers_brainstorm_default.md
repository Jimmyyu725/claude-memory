---
name: feedback_superpowers_brainstorm_default
description: "开始新项目/新功能前默认自动用 superpowers:brainstorming 理清意图再动手,后接 plan→TDD→verify 流程"
metadata:
  node_type: memory
  type: feedback
---

**默认:开始一个新项目 / 新功能 / 较大改动前,先自动调用 `superpowers:brainstorming` skill**,把意图、需求、设计理清楚再写代码——不用等用户点名。用户 2026-06-17 装了 superpowers 插件并要求把这套"先想清楚再做"作为默认流程。

**Why**:质量更稳(先对齐意图、少返工);`superpowers:brainstorming` 本身就要求"任何创作工作前必用"。

**How to apply**:
- 触发场景:新功能/新项目/较大重构启动时 → 先 `Skill superpowers:brainstorming`。
- **不必**用在:小修小补、改字/改样式、纯问答、明确的一次性机械操作(免得啰嗦)。
- 配套流程:`brainstorming → superpowers:writing-plans → test-driven-development → verification-before-completion`(声称"做好了"前先跑命令验证、拿证据)。
- 这是行为偏好(靠我自觉 + skill 自身触发),不是 settings.json 里的确定性 hook。
- 关联 superpowers 一整套 skill;记忆同步见 [[reference_memory_git_sync]]。
