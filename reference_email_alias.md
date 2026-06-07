---
name: reference_email_alias
description: 用户的邮箱别名方案——自有域名 jimmyyu888.com 做 catch-all 转发到 Gmail
metadata: 
  node_type: memory
  type: reference
  originSessionId: a39b3580-cb9a-4512-bf43-dd8386fa390e
---

用户 2026-06-06 搭好的隐私邮箱别名方案:

- **域名**:`jimmyyu888.com`(在 **Cloudflare Registrar** 注册,$10.46/年,续费同价,WHOIS 已隐藏)
- **机制**:Cloudflare **Email Routing catch-all** → `任意@jimmyyu888.com` 全部转发到真邮箱 `y326433462@gmail.com`
- **用法**:注册网站时填 `网站名@jimmyyu888.com`(不用预创建,catch-all 全收);某前缀收到垃圾 → 知道是哪个网站泄露/卖了信息
- **限制(重要)**:catch-all **只收不发**;要回复客服会露真 Gmail。需双向对话的场景改用 **DuckDuckGo Email Protection**(支持反向别名回复,真邮箱不露)
- Gmail 侧建议设过滤器:To=`@jimmyyu888.com` → 从不进垃圾箱 + 打标签,防验证码漏收

教过用户的概念:Gmail 加号别名(`name+tag@gmail.com`,易被去后缀)< 别名服务(DuckDuckGo/SimpleLogin,可关可回复)< 自有域名 catch-all(本方案,最自由);"用 Google 登录"会直接暴露真 Gmail,别名那套对它无效,在意隐私就走邮箱注册或 Apple 隐藏邮箱。
