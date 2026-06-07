---
name: galgang-unity-mcp
description: "用户的 Unity 6 工程 \"GalGang\" 及其 Unity MCP ↔ Claude Code 接入配置"
metadata: 
  node_type: memory
  type: project
  originSessionId: 6666de14-cb08-4621-ae4b-c68b8a45932a
---

用户有一个 **Unity 6 工程 "GalGang"**,路径 `F:\Unity Engine\Unity Project\GalGang`(由 `UserSettings\mcp.json` 路径确认)。这是独立于 [[doomfollow-game]](MonoGame,不用 Unity)的另一个项目。

已配置 **Unity MCP**(`com.unity.ai.assistant` 包,要求 Unity 6+)让 Claude Code 直接操控 Unity 编辑器:
- 中继程序(relay):`C:\Users\y3264\.unity\relay\relay_win.exe`(全局安装,随 Unity 启动)
- 注册方式:`claude mcp add --scope user --transport stdio unity-mcp -- C:\Users\y3264\.unity\relay\relay_win.exe --mcp`(**user 作用域**,写在 `C:\Users\y3264\.claude.json`)
- Unity 侧入口:`Edit > Project Settings > AI > Unity MCP Server`(Unity Bridge 要显示绿色 Running;`Tools` 区里要勾选允许 Claude Code 调用的工具,默认只开 7/52)
- 已勾选的核心工具:ManageGameObject / ManageScene / CreateScript / ManageScript / ScriptApplyEdits / DeleteScript / ManageAsset / FindInFile / Grep / 场景截图(SceneView_Capture)等

**How to apply:** 要让 Claude Code 拿到 Unity 工具,Unity 必须开着 GalGang 工程且 Bridge 为 Running;新增 unity-mcp 后,**当前已运行的 Claude Code 会话不会热加载,必须重启**(最好从 GalGang 目录启动)。首次连接时 Unity 若弹 "Pending Connection" 需在该页面点 Accept,之后 Connected Clients 会显示客户端。
