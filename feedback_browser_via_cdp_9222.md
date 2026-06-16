---
name: feedback_browser_via_cdp_9222
description: "浏览器自动化/搜索默认连常驻 chrome-cdp(127.0.0.1:9222),不要新开 Chrome;不可信浏览用隔离 incognito 上下文"
metadata:
  node_type: memory
  type: feedback
---

**默认:任何浏览器自动化/网页搜索/抓取都连接常驻的 chrome-cdp(`127.0.0.1:9222`),不要自己起一个新的 Chrome。** 用户 2026-06-16 确认这是默认偏好。

**Why**:9222 是常驻 headless Chrome(`chrome-cdp.service`,带登录态 profile:Google/Ctrip/Booking 等),已在跑。复用它=自动带登录态、省启动开销、单实例不留孤儿 Chrome 进程。每次新开 Chrome 既浪费又会和这个 profile 抢锁。

**How to apply**:
- 连接:`puppeteer.connect({ browserURL: 'http://127.0.0.1:9222' })`(或 Playwright `connectOverCDP`)。**永不** `puppeteer.launch()` / 直接 `google-chrome` 起新实例。
- **需要用户登录态**的任务(订票、Booking、Google 等)→ 用默认上下文(已登录)。
- **普通搜索 / 访问不可信网站** → 在**同一个 9222 浏览器**里开隔离上下文 `const ctx = await browser.createBrowserContext()`(incognito),用 `ctx.newPage()`,**用完 `ctx.close()`**;避免污染登录 profile 的 cookie/历史,也避免把登录态暴露给恶意页面。
- 用完**关页面/上下文**,别让标签页堆积。
- **互斥**:`chrome-cdp` 和交互式 `chrome-login` 不能同时开(Chrome profile 单例锁)——要交互登录得先停 chrome-cdp。
- 服务已加固:开机自启 + `Restart=always` + 启动时自动清理残留 Singleton 锁。详见 [[project_claude_console]] 同机的 jimmynas-handoff.md。
