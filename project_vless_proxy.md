---
name: project-vless-proxy
description: 用户自建的私人代理（VLESS+Reality on Vultr Tokyo），备忘在桌面
metadata: 
  node_type: memory
  type: project
  originSessionId: 544b7463-df15-47b3-9f5f-332061f9fa27
---

用户已搭好一台**私人代理**：Vultr 东京机房、Ubuntu、Xray-core、VLESS + Reality + TCP（flow xtls-rprx-vision）。

客户端：Windows 上用 **v2rayN**（`v2rayN-windows-64-desktop.zip`），iOS 上用 Shadowrocket。

完整连接参数 + 服务器命令 + 排错都记在 `C:\Users\y3264\Desktop\VLESS-Reality-备忘.md`（含真实密钥，**敏感文件，别截图/上传/外传；私钥仅服务器用**）。原始教程在 iCloud `下载iCloud\VLESS-Reality-搭建教程.md`。

**Why:** 跟 [[user_nccu_exchange]]（2026 秋去台湾交换）相关，代理是为出国/去大陆时换 IP、解锁地区内容用。
**How to apply:** 以后他问"代理连不上/换节点/加新设备"，直接看那份桌面备忘；排错先查防火墙 443（他上次就栽在 ufw 没放行 443）。涉及 key 时遵守 [[feedback_api_key_security]] 思路——只验证、不打印明文。
