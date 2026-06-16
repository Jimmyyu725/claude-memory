---
name: project_claude_console
description: "Claude Console——code.jimmyyu888.com 上 ttyd 终端前面的会话管理器(列出/进入/暂停/删除/远程控制 tmux 里的 Claude 会话),2026-06-15 自建"
metadata:
  node_type: memory
  type: project
---

**Claude Console**(2026-06-15 建):门户的 "Claude Code CLI" 卡片现在打开的不是裸终端,而是一个**会话列表页**(像 Claude Desktop),每个 tmux 会话一张卡:名字、`status:Running🟢/Paused🟡`、**Pause/Resume**(琥珀,真冻结)、**Delete**(红,kill)、底部 **Remote-control: ON/OFF** 开关;点名字 / Open terminal 进全屏终端覆盖层(ttyd 装在 iframe 里)。顶部 **+ New session** / **Continue last**(`claude --continue`)。

**架构**(全在 jimmynas,不在容器):
- 后端 `claude-console.service`(systemd,User=jimmy,绑 `127.0.0.1:7682`)= `/srv/appdata/claude-console/server.py`(纯 Python stdlib,无依赖)。既出 JSON API(`/api/sessions` 列表、POST 新建、`/<name>/pause|resume|remote`、DELETE 删)又托管 `./site` 静态 SPA。
- 前端 `/srv/appdata/claude-console/site/`(index.html + js/app.js + css/app.css,vanilla JS)。改 app.js 记得 bump `?v=N`。
- Caddy `@code` 块:`/t-jx9mQ4wRk7/*`→7681(ttyd),其余→7682(console),整体仍在 `remote_ip 100.64/10 192.168/16 127.0.0.1/8` 白名单后(仅 LAN/Tailscale)。
- 门户卡片来自 `dashboard/homepage-config/services.yaml`(门户复用 homepage 的 `/api/services`);已指向 `https://code.jimmyyu888.com/`、描述 `session manager on jimmynas`。

**Pause = cgroup v2 freezer**(关键):tmux 会把 `SIGSTOP` 暂停的 pane 进程在 ~50ms 内自动 `SIGCONT` 复活,所以唯一可靠的真暂停是 cgroup freezer。root 助手 `/usr/local/bin/claude-session-freeze <freeze|thaw> <name>`(仅冻结/解冻、`tr -cd` 校验会话名、从 jimmy 的 tmux 自解析 pid、不接受外部 pid、无法 kill/跑任意命令)+ `/etc/sudoers.d/claude-console`(jimmy 仅对该脚本 NOPASSWD)。状态检测读 `/sys/fs/cgroup<pane-cgroup>/cgroup.events` 的 `frozen` 标志。Delete 先 thaw 再 kill,避免遗留空 sess cgroup。

**Remote-control 开关**是尽力而为:点它向会话 `send-keys /remote-control <名字>` 并打开终端去完成配对;ON/OFF 徽标只反映"本进程内是否发过"(真正开关在会话内,后端重启后标志清零)。

**标题统一(2026-06-16)**:Console 卡片名、会话 `-n` 显示名、远程控制 App 标题三者一致。关键 CLI 参数:`-n <name>`(显示名=终端标题+resume 选择器)、`--remote-control [name]`(可命名,否则 `--remote-control-session-name-prefix` 默认=主机名,所以默认是 `jimmynas-随机词`)。实现:`session_cmd` 加 `-n <display>`(主会话=`main`,其余=label);remote 端点发 `/remote-control <display>`;`/usr/local/bin/claude-web-term` 也加了 `-n`(默认→`main`,`?arg=NAME`→`NAME`)。`/remote-control <name>` 斜杠命令实测认名字参数。

关联 [[project_pihole]]、[[project_jimmy_drive]];与已下线的 [[project_claudeweb]] 无关(那是另一回事)。两个底层 tmux/Docker 硬坑见 jimmynas-handoff.md 的 Gotchas 段。
