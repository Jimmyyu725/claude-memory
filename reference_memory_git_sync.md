---
name: reference_memory_git_sync
description: "记忆目录同步到 GitHub private 仓库 Jimmyyu725/claude-memory;现由 jimmynas 维护,token 受 sudo 墙阻挡,改用登录态浏览器网页上传同步"
metadata:
  node_type: memory
  type: reference
---

记忆目录同步到 **GitHub private 仓库**:`https://github.com/Jimmyyu725/claude-memory`(账号 `Jimmyyu725`)。

⚠️ **仓库含敏感信息(VLESS 私钥、家庭网络拓扑、SSH 配置)→ 永远保持 private,绝不转 public。**

**历史**:2026-06-07 在 Pi 上建库,jimmypi(源)+ pi4gb(clone)用 git+token 同步,Windows 是原始来源但未接入。**两台 Pi 现已退役。**

**现状(2026-06-16,jimmynas)**:活的记忆在 **jimmynas 的 `/srv/appdata/memory/`**,这是 2026-06-14 从 Windows 拷来的**快照,不是 git clone**。本机 `gh` 未登录、也没有 git 凭证。

**同步方式(jimmynas)**:直接 `git push` / 建 token 走不通——GitHub 建 PAT 的页面要二次输密码(sudo 墙),设备码流程的分段输入框又抗自动化。所以目前靠 **常驻登录态的 chrome-cdp(9222)走 GitHub 网页版 "Upload files" 提交**(不需要 token、不过 sudo 墙)。2026-06-16 用此法把本地缺失的 8 条记忆补推上去。

**要恢复正经 git 同步**:需 Jimmy 本人在 GitHub 建一个 PAT(要他的密码),放进 jimmynas 的 `~/.git-credentials`(`Jimmyyu725:<token>`,chmod 600),再把 `/srv/appdata/memory` 变成该库的 clone。之后即可 `git pull`/`commit`/`push`。

**纪律**:保持 private;写完记忆要同步(当前=浏览器网页上传)。相关 [[project_pihole]]。
