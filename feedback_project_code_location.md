---
name: feedback_project_code_location
description: 所有项目代码统一放 C:\Project\ 子文件夹;Claude Code 自身配置除外
metadata: 
  node_type: memory
  type: feedback
  originSessionId: 3cd90ee5-ec49-45b2-841c-3f96b668c0bc
---

`C:\Project\` 是**默认/兜底**的代码根目录：当用户随手开一个新项目、且没有指定具体位置时，就在这里建一个子文件夹，按内容用简短命令式名字命名（如 `moomoo-monitor`、`facepack-gen`），该项目之后的所有代码都进这个子文件夹，不乱放。

**不放进 `Project\` 的情况：**
1. **Claude Code 自身的配置** —— `~/.claude/` 下的 settings、skills、hooks、memory 等，不算项目代码。
2. **本身就该有自己专属文件夹的项目** —— 比如 Unity（以及其他有自己工程结构/默认存储位置的程序、引擎、IDE）。这类项目放到**该程序为它设置的默认存储位置**，不要塞进 `Project\`。
3. **用户指定了具体路径时** —— 听用户的，放到指定位置。

**Why:** 用户要整洁的代码根目录，但有专属工程结构的东西硬塞进来反而会乱；`Project\` 只是没有更合适位置时的默认落点。

**How to apply:** 写项目代码前判断——有指定路径→用指定；是 Unity/有自己工程目录的程序→用它的默认位置；是 Claude Code 配置→`~/.claude/`；以上都不是（随手开的普通项目）→默认 `C:\Project\<短名>\`。
