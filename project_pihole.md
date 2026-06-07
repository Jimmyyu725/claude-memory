---
name: project_pihole
description: Pi 4 树莓派项目——原计划 Pi-hole,已改向"自建家庭小服务器"
metadata: 
  node_type: memory
  type: project
  originSessionId: a39b3580-cb9a-4512-bf43-dd8386fa390e
---

**⚠️ 方向已变(2026-06-05)**:用户决定**不做 Pi-hole 去广告了**,把这块 Pi 4 2GB **改做自建家庭小服务器**(Docker 跑 Portainer + Vaultwarden + Gitea + Tailscale + Homepage 入门栈)。新方案:`C:\Project\PiServer\PROJECT-PLAN.md`。下面是历史背景:

用户 2026-06 原本的家庭网络动手项目:树莓派跑 **Pi-hole**,全家设备 DNS 级去广告 + 网页统计面板。

关键决定:
- 选型 = **Pi 4 2GB**(我替用户拍板)。理由:常开 DNS 盒子要**网口**才稳(WiFi 不靠谱),2GB 留扩展余地。
- **明确否决 Pi 5 8GB 套件($260)**:Pi-hole 很轻,杀鸡用牛刀 + 2026 内存涨价坑。(注:DonkeyCar/AI 自驾车项目用户后来也放弃了,已删除。)
- 超省备选 = Pi Zero 2 W($15,WiFi only)。
- **硬件(两块 Pi 4,都已到货保留)**:CanaKit **4GB PRO** $161.98 + CanaKit **2GB** $145.79;Zero 2 W 已取消。
  - ⚠️ 用户最终**翻转了分配**:**2GB = 家庭服务器主力**(理由"大内存留给实验");**4GB = 沙盒/重型实验机**(物体识别等,`C:\Project\PiSandbox\NOTES.md`)。

## ✅ 服务器已建成(2026-06-06)
- 这台 = **2GB Pi**,主机名 **jimmypi**,局域网 IP **192.168.1.22**,走 WiFi "Jimmy's"。系统 Raspberry Pi OS Lite 64-bit,用户 `jimmy`(密码用户自设)。
- **Claude 有免密 SSH 管理权**:私钥 `C:\Users\y3264\.ssh\pi_key`(无 passphrase),连法:`ssh -i "$env:USERPROFILE\.ssh\pi_key" -o IdentitiesOnly=yes -o BatchMode=yes jimmy@jimmypi.local "<cmd>"`;且 **sudo 免密**。→ 以后我可直接帮用户管这台 Pi。
- Docker 栈在 `~/docker/docker-compose.yml`(数据 bind mount 到 `~/docker/<服务>`),全部 HTTP 200:
  - Portainer `:9000`(+`:9443` https)/ Vaultwarden `:8080` / Gitea `:3000`(git-ssh `:2222`)/ Homepage `:3001`
- **Tailscale 已连**:tailnet `tail90a957.ts.net`(账号 google@jimmyyu888.com 那个小号),Pi 节点名 jimmypi,Tailscale IP **100.94.233.2**;iPhone(iphone172)也已加入。MagicDNS + HTTPS 证书已启用。
- **Vaultwarden 已配 HTTPS**:`sudo tailscale serve --bg 8080` 反代 → **https://jimmypi.tail90a957.ts.net**(HTTP 200,正规证书);手机用官方 Bitwarden App 指向该 URL。待用户注册账号后应把 compose 里 `SIGNUPS_ALLOWED` 改回 false。
- Exit node 尚未开(用户想要"出国变芝加哥 IP"时再 `tailscale up --advertise-exit-node` + 后台批准)。
- 注:首次 apt full-upgrade 后 jimmy 的免密 sudo 文件丢失,已重建 `/etc/sudoers.d/010_jimmy-nopasswd`。
- 踩过的坑:CanaKit 原装卡没烧需用 Imager 烧 Lite;`ssh-keygen -N '""'` 在 PS7 会给私钥设密码(要 `-N ''`),且 icacls 设只读会导致改不动 key。

## ✅ 4GB 沙盒机也建好了(2026-06-06)= 摄像头物体识别
- 这台 = **4GB Pi**,主机名 **pi4gb**,用户 **jimmy4g**,局域网 IP **192.168.1.23**,走 WiFi "Jimmy's"。系统 **Raspberry Pi OS (64-bit) with desktop / Debian 13 trixie / Python 3.13**(带桌面,因为要本机 HDMI 屏看视频窗口)。桌面是 **labwc(Wayland)**,显示用 **kanshi** 管(配置 `~/.config/kanshi/config`,已锁 **1920x1080@60**,原本默认 4K 太重)。
- **Claude 有免密 SSH + 免密 sudo**:同一把私钥 `C:\Users\y3264\.ssh\pi_key`,连法 `ssh -i "$env:USERPROFILE\.ssh\pi_key" -o IdentitiesOnly=yes -o BatchMode=yes jimmy4g@pi4gb.local`。sudoers 免密文件 `/etc/sudoers.d/010_jimmy4g-nopasswd`。(首次连接用密码装的密钥;Windows 上为非交互登录装了 PowerShell 的 **Posh-SSH** 模块,能用密码自动登录。)
- **Pi→Pi 免密(2026-06-07 配)**:从 jimmypi(2GB)可直接 `ssh pi4gb` 连到这台。在 jimmypi 上生成了专用密钥 `~/.ssh/pi4gb_key`(ed25519,无密码),公钥已加进 pi4gb 的 `~/.ssh/authorized_keys`(当时借 Windows 的 pi_key 远程追加);jimmypi 的 `~/.ssh/config` 配了 `Host pi4gb`(→192.168.1.23, User jimmy4g)。→ Claude 在 jimmypi 会话里可直接管 pi4gb。
- **摄像头**:Logitech **Brio 100**(USB,046d:094c)→ `/dev/video0`,UVC 即插即用。
- **物体识别项目**:本地工程 `C:\Project\PiCam\`(detect.py / cap_test.py / run.sh / kanshi_config),部署到 Pi 的 `~/cvcam/`。方案 = **OpenCV DNN(apt python3-opencv 4.10)+ YOLOv4-tiny**(纯系统 OpenCV,不碰 pip,避开 Py3.13 轮子坑;认 80 类 COCO;Pi4 上 ~5-8 FPS)。模型在 `~/cvcam/models/`(yolov4-tiny.cfg/.weights/coco.names,从 AlexeyAB/darknet 下)。
- **启动方式**:用 systemd 用户服务(GUI 程序送上 HDMI 桌面最稳):`systemd-run --user --unit=cvcam-detect --setenv=WAYLAND_DISPLAY=wayland-0 --setenv=DISPLAY=:0 --setenv=XAUTHORITY=/home/jimmy4g/.Xauthority --setenv=GDK_BACKEND=x11 --working-directory=/home/jimmy4g/cvcam python3 -u /home/jimmy4g/cvcam/detect.py`(先 `export XDG_RUNTIME_DIR=/run/user/1000; export DBUS_SESSION_BUS_ADDRESS=unix:path=/run/user/1000/bus`)。停:`systemctl --user stop cvcam-detect`。窗口里按 q 退出。**注意**:直接 `nohup ... &` 后台启动会被 ssh 断开杀掉(日志空),必须 systemd-run 或 setsid。
- 调灵敏度:环境变量 `CONF`(默认 0.4)。

## ✅ 升级成"便携 AI 视觉语音助手"(2026-06-06)= 当前主玩法
用户把 4GB Pi **装进便携盒子**(电池/3.5mm小音箱/USB Brio摄像头),做成随身"能看能聊"的盒子:举起来对它说话问"这是什么",它看一眼用语音回答。
- **链路**:Brio 麦克风(card 3,`plughw:CARD=B100,DEV=0`)→ 能量VAD检测说话 → Whisper(whisper-1,强制 `language=zh`)转文字 → gpt-4o-mini 看摄像头当前帧 → tts-1 合成 → `pw-play` 走 **3.5mm 耳机孔**(PipeWire 默认 sink)念出来 → "叮咚"提示音 → 回到待命。全用用户自己的 OpenAI key(`~/cvcam/.env`,chmod600,从 Windows `.env.local` 安全传入,never print)。
- **代码**:本地 `C:\Project\PiCam\`,部署到 Pi `~/cvcam/`。核心 `assistant_live.py`(常驻待命版,requests 直连 REST,避开 Py3.13 轮子坑);`run_live.sh` 启动器;`assistant.py`(按键版)/`selftest.py`/`level_meter.py`/`beepgen.py` 辅助。venv 在 `~/cvcam/venv`(--system-site-packages 复用系统 cv2,只 pip 装了 requests)。
- **开机自启**:正式 user 服务 `~/.config/systemd/user/cvcam-assistant.service`(WantedBy=default.target,ExecStartPre sleep 8,Restart=on-failure,Environment 里设阈值)。已 `enable`,**真重启验证过自动待命**。桌面自动登录(raspi-config autologin=0)保证 PipeWire 就绪。控制:`systemctl --user start/stop cvcam-assistant`(先 export XDG_RUNTIME_DIR=/run/user/1000)。日志 `~/cvcam/assistant.log`。
- **调参(都是 systemd Environment / env)**:`START_THR`(触发,当前 800)、`STOP_THR`(停顿 550)、`MIN_VOICED`(10)、`VOICED_RATIO`(0.35,挡尖峰杂音)、`MAX_TOKENS`(80,答案≤25字更快)、`HEARTBEAT`(调试音量心跳)、`BEEP`(就绪提示音)。音量:`wpctl set-volume @DEFAULT_AUDIO_SINK@ 0.45`。
- **踩过的坑/经验**:① Whisper 在空音频会幻觉"谢谢观看/thanks for watching/日文",靠"有声占比+假名检测+黑名单+长音频却超短文字"过滤;② 纯能量VAD在有底噪房间要调阈值(实测安静≈300-540,说话700-2000);③ 边说边打断(barge-in)做不了(单麦挨音箱无回声消除),用"叮"提示音+短回答缓解;④ 拍照用 `cap.grab()×3 + retrieve()` + `CAP_PROP_BUFFERSIZE=1` 把 0.98s 降到~0.3s;⑤ 临时文件放 `~/cvcam/tmp` 用完即删;⑥ GUI/音频程序从 SSH 启动必须用 systemd user 服务或 setsid,直接 `nohup &` 会被 ssh 断开杀掉;⑦ mDNS `pi4gb.local` 偶尔解析失败,用 IP 192.168.1.23 兜底。
- **典型耗时**:说完→出声 ~3-5s(STT~1.5+看图~1.3+合成~1-3),识别很准(认出折叠键盘、中/美护照、乒乓拍、手机读屏上时间)。

教过用户的概念:Pi-hole 是 DNS 级拦广告(全设备/含App,但**挡不住 YouTube** 同域名广告,需配 uBlock Origin);单点故障要在路由器留备用 DNS 1.1.1.1;云端替代方案是 NextDNS/AdGuard DNS(零硬件)。

方案文档:`C:\Project\PiHole\PROJECT-PLAN.md`。
此前还评估过:把 Pi-hole 装在用户现有的 Vultr VPS([[project_vless_proxy]])上(WireHole),用户最终选了树莓派路线。
