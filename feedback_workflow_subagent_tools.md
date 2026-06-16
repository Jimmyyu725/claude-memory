---
name: feedback-workflow-subagent-tools
description: "后台自主模式下,工作流子 agent 的联网工具会被权限拒绝而卡死;联网核验要在主线程做"
metadata: 
  node_type: memory
  type: feedback
  originSessionId: 85be0f6f-52ce-425c-8880-034f2c4eea1f
---

在后台/自主运行的 Workflow 子 agent 里,需要授权的工具(尤其 **WebSearch / WebFetch**)会被**自动拒绝**(`User rejected tool use` / `[Request interrupted]`),子 agent 随即停下等指令,整个工作流静默卡死。只读工具(Read / Grep / Glob)在子 agent 里正常。

**Why:** 后台没有人能点"允许"权限弹窗,联网工具默认拒绝。2026-06-07 做 [[project-gesture-seek]] 时,7 个联网核验子 agent 同一秒全部冻结,排查日志才发现。

**How to apply:**
- 需要联网的核验/研究,**在主线程亲自调 WebSearch/WebFetch**(主线程有权限),不要丢给工作流子 agent。
- 工作流子 agent 只派**纯本地只读**任务(读代码、审查、grep),它们能正常跑(代码审查 13 个并行 agent 验证可行)。
- 派子 agent 前,若任务含联网/写操作,先想清楚权限会不会被拒。
