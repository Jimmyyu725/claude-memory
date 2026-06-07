---
name: project-doomfollow-game
description: "《末日追随》2D 横版僵尸射击游戏(C#/MonoGame),位置与技术栈"
metadata: 
  node_type: memory
  type: project
  originSessionId: 0ab2c3ea-406c-4595-90d5-bcba3f13f30e
---

《末日追随 / DoomFollow》——用户让我做的 2D 横版卷轴僵尸射击游戏(Broforce 风格),2026-06-02 完成第一个可玩版本。

- **位置**:`C:\Project\DoomFollow`(符合 [[feedback-project-code-location]] 的 Project\ 默认落点)
- **技术栈**:C# + MonoGame.Framework.DesktopGL 3.8,目标 net9.0,用 .NET 10 SDK 构建。**不用 Unity**(用户明确要求纯代码生成场景/物品/行为)。
- **美术**:用 `gpt-image-1.5` 一次性生成精细像素 PNG 存到 `Assets/`,运行时 `Texture2D.FromStream` 加载;缺图自动退回几何占位。重生成脚本在 `tools/`。见 [[reference-gpt-image-transparency]]。
- **运行**:`dotnet run --project C:\Project\DoomFollow\DoomFollow.csproj`。操作 A/D 移动、空格跳、J/鼠标开火、R 重开。

**Why:** 用户不是 C#/WPF 开发者([[user-profile]]),后续若继续做这个游戏,需要知道它在哪、用什么、怎么跑。
**How to apply:** 继续迭代时直接在该目录改代码;加美术用 `tools/gen-sprite.ps1`;第一版玩法/架构见 `docs/specs/2026-06-02-doomfollow-design.md`。
