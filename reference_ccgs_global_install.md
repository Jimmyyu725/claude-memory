---
name: reference-ccgs-global-install
description: Claude-Code-Game-Studios 的 skill/agent 已全局安装到 ~/.claude
metadata: 
  node_type: memory
  type: reference
  originSessionId: 0ab2c3ea-406c-4595-90d5-bcba3f13f30e
---

用户把 [Claude-Code-Game-Studios](https://github.com/Donchitos/Claude-Code-Game-Studios) 这套"游戏工作室"工作流**全局安装**了(2026-06-02):

- 克隆在 `C:\Project\Claude-Code-Game-Studios`(完整模板:含 hooks/rules/docs/templates,项目级配置)。
- **73 个 skill → `~/.claude/skills/`**、**49 个 agent → `~/.claude/agents/`**(全局,故每个会话都会多出这些游戏开发 skill)。
- 为避免撞车,两个 CCGS skill 改了名:`code-review`→`ccgs-code-review`、`help`→`ccgs-help`(把内置 `/code-review`、`/help` 让回来)。

注意:这些 skill 为完整 CCGS 工程设计(引用 `design/gdd/`、`production/`、`docs/architecture/`、`.claude/docs/` 等),在普通文件夹里只能半残;完整功能需在 CCGS 工程内用。面向 Godot/Unity/Unreal,与纯 MonoGame 的 [[project-doomfollow-game]] 方向不同。
