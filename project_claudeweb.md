---
name: project_claudeweb
description: "ClaudeWeb 网页版 Claude Code——已于 2026-06-11 整体下线(从未真正启用),用户决定直接用 Claude Code CLI;代码仓库保留"
metadata:
  node_type: memory
  type: project
  originSessionId: f978d678-1afc-474c-9ab6-9a8bc64f9c32
---

**ClaudeWeb 已下线(2026-06-11,建成当天)**:用户决定"这条路删除,直接走 Claude Code CLI"。服务从未真正用过(`ANTHROPIC_API_KEY` 一直没填)。

- **已移除**:jimmypi 上的 claudeweb 容器、compose 段、Caddy `@code` 路由(code.jimmyyu888.com 现 404)、门户卡片、1.44GB 镜像 + 3.7GB 构建缓存(SD 卡 13G→8.5G)、`~/docker/claudeweb/`(含 .env)。DNS 无需动(走的是 `*.jimmyyu888.com` 通配符,其他服务共用)。
- **保留**:代码仓库 `C:\Project\ClaudeWeb` + Gitea `jimmy/ClaudeWeb`(归档,想复活随时能起)。
- **沉淀的合规结论仍有效**:Agent SDK 无头只能 API key;订阅 OAuth 跑无头违反 Consumer Terms §3.7;单人自建 + API key 合规(Commercial §A.1/§B)。
- 用户 Vaultwarden 里那条 ClaudeWeb 密码(river-quartz-falcon-saffron-86)可删。
- 关联 [[project_pihole]]、[[feedback_api_key_security]]。
