---
name: reference_memory_git_sync
description: 记忆目录已做成 GitHub private 仓库,三机用 git 同步
metadata:
  type: reference
---

记忆目录 `~/.claude/projects/C--/memory/`(在 Pi 上)做成了 **GitHub private 仓库**,用 git 在多机间同步(2026-06-07 配,方案选 GitHub 而非自建 Gitea)。

- **远端**:`https://github.com/Jimmyyu725/claude-memory`(**private**,GitHub 账号 `Jimmyyu725`)。⚠️ 库里含敏感信息(VLESS 私钥、家庭网络拓扑、SSH 配置),**永远保持 private,绝不转 public**。
- **已接入的机器**:
  - **jimmypi**(2GB,本仓库源):`~/.claude/projects/C--/memory` 即 git 仓库;`gh` 已登录(token 在 `~/.config/gh/hosts.yml`)。
  - **pi4gb**(4GB):同目录是该库的 clone;git 凭证存在 `~/.git-credentials`(`Jimmyyu725:<token>`,chmod600)。
  - **Windows 主机**:原始记忆来源,**尚未接入**;要同步需在 Windows 上 `git clone` 该库到 `C:\Users\y3264\.claude\projects\C--\memory`(覆盖前先备份原目录)。
- **同步纪律(手动)**:改记忆前 `git pull`,改完 `git add -A && git commit && git push`。不是实时,需养成习惯;Claude 写完记忆应顺手 commit+push。
- 相关:两台 Pi 见 [[project_pihole]];Pi 间免密 ssh 也在那条里。
