---
name: project_jimmy_drive
description: "Jimmy Drive 自研网盘前端 + 玻璃拟态门户——repo C:\\Project\\JimmyDrive;前端静态仍由派 Caddy 伺服,后端 filebrowser+数据已迁到 NAS(2026-06-14)"
metadata: 
  node_type: memory
  type: project
  originSessionId: f978d678-1afc-474c-9ab6-9a8bc64f9c32
---

**Jimmy Drive(2026-06-10 一天建成)**:用户嫌 Filebrowser Quantum 原版 UI 丑,在其 REST API 上纯手写了百度网盘式前端。**内核不动、只换皮**的模式用户极其喜欢,后来门户也照此办理。

- **⚠️ 大半已迁到 NAS(2026-06-14,详见 [[project_pihole]])**:filebrowser(Quantum)+ 数据 `/srv/fileshare` + SilverBullet + **Homepage + 门户** 现跑在 **jimmynas**(`100.67.108.78`)。端口:filebrowser `:8081`、silverbullet `:3030`、homepage `:3001`、门户 nginx `:8088`(后两个 compose 在 NAS `/srv/appdata/dashboard/`,前两个在 `/srv/appdata/drive-stack/`)。**只有 Drive 前端 UI(`app/`)还由派 Caddy file_server 伺服**;`deploy.ps1` 已拆:`app/`→派 `~/docker/caddy/site/drive`,`portal/`→NAS `:/srv/appdata/dashboard/portal`。派 Caddy(仍是 TLS/域名总入口)把 `/drive/api|public|share`、`files.`、`notes.`、`/api/*`、门户根 `/` 全反代到 NAS 对应端口。派上旧容器(filebrowser/silverbullet/homepage)已 stop 可回滚;派 `/srv/fileshare` 原数据留作加密备份。门户存储条改成动态取真实总量(不再写死 229G,commit 9465d22)。

- **Repo**:`C:\Project\JimmyDrive`(git,master)。**远端 = 用户自家 Gitea**:`ssh://git@192.168.1.25:2222/jimmy/<repo>.git`(JimmyDrive 的 remote 叫 `origin`,其余 9 个项目都叫 `gitea`;push 时 `GIT_SSH_COMMAND` 指定 pi_key,Gitea 账号挂了公钥 "claude-pc")。**铁律(2026-06-11 用户定):`C:\Project` 下所有项目 commit 后必 push 到 Gitea,本地仍是工作目录**——10 个仓库已全部镜像(含 MiroFish/DoomFollow/PiCam 等;MiroFish 的 .env 从未入库,已验)。Gitea 开了 **push-to-create**(`ENABLE_PUSH_CREATE_USER`,默认 Private):新项目直接 push 即自动建仓,无需网页操作。Gitea 已升 HTTPS `https://git.jimmyyu888.com`(进通配符证书块,ROOT_URL 已同步,旧 http 入口 301)。`app/` = 网盘前端(vanilla ES modules,零构建零依赖,预览库 vendored);`portal/` = 门户单文件;`tests/contract.ps1` = 接口回归(跑法 `-Username admin -Password <pw>`);`deploy.ps1` = 一键 scp 到 Pi(网盘→`~/docker/caddy/site/drive`,门户→`.../portal`,Caddy file_server 伺服,改完即生效)。
- **网址**:网盘 `http://drive.jimmyyu888.com`(账号同 Filebrowser admin);门户 `http://jimmyyu888.com`(玻璃拟态,Homepage 容器降级为数据内核:`/api/services`+`/api/widgets/resources`,AdGuard 统计经 Caddy 注入 Basic 头代理 `/adguard/*`);原版 UI `files.jimmyyu888.com` 留作后台(管 API token/账号用)。
- **功能全集**:浏览/缩略图/排序/网格、上传队列(进度条+拖拽)、下载/打包 zip、重命名/移动/复制(事前查重名弹"替换"确认)、**回收站**(`/.trash`,文件名前缀 `<unixms>__`,可恢复/清空)、分享管理页、Recent(7 天)、分类(图/文档/视频/音频/压缩包+Type 列)、全盘搜索、预览(图/视频/音频/PDF/MD/docx/CSV/代码,50MB 文本守卫,iOS PDF 开新页)、暗夜模式(System/Light/Dark,设置齿轮里)、Explorer 式选择(单击单选/Ctrl 加选/Shift 范围/双击打开/勾选列扫选/拖拽行→文件夹或面包屑=移动)、右键上下文菜单(含 Details)、手机端长按划选+FAB。
- **Quantum API 硬经验**(都实测过):建目录必须 `isDir=true`(尾斜杠会建出 0 字节文件);**move/copy 的 overwrite=false 不报冲突而是静默覆盖**(所以 UI 必须事前 listDir 查重名);并发搜索会互相清空(**每请求带唯一 SessionId 头**);搜索结果 path 无前导斜杠、目录带尾斜杠;目录在 listing 的 `folders[]` 数组且 size 是真实递归大小;`?auth=<token>` 查询参数可代 Bearer(img/iframe 用);搜索 query 最少 2 字符,`type:` 过滤无效,`newerThan`(unix 秒)有效;搜索索引持久在 `data/tmp/sql/`,Samba 侧删文件后会留幽灵,清法 = 停容器→挪走 sql 目录→启动重建。
- **HTTPS**:`*.jimmyyu888.com` 通配符 + 裸域名证书都有(caddy-cloudflare:local + CF token,见 [[project_pihole]]);**网盘正式地址 `https://jimmyyu888.com/drive/`**(真路径部署:filebrowser baseURL=/drive,文件夹/文件都进 URL、可深链接直达预览;旧 drive. 子域名 301)。主域名还有路径跳转 /vault /git /portainer /adguard /files。
- **v2.0(2026-06-10 深夜定稿,git tag v2.0,52 commits)**:大厂级设计系统(Inter 字体 vendored、电光蓝紫渐变唯一强调色、毛玻璃浮层、160ms 统一动效、亮暗双主题);右键菜单含 **Copy image(剪贴板写真图,需 HTTPS)**/Copy link/Details;Explorer 式选择(单击单选/Ctrl/Shift/双击打开/勾选列扫选/拖拽行到文件夹=移动);视频缩略图带**时长角标**(/api/media/metadata 的 metadata.duration 秒);**HEIC 浏览器内解码**(vendor/libheif.js 新版,await libheif() 工厂→HeifDecoder;服务器 ffmpeg 转 HEIC 会出碎瓦千万别开 integrations.media.convert.imagePreview.heic)。
- **移动端上传(已彻底修好)**:两个 iOS 快捷指令(主页版选 Photos/Files + 分享版),全走 `https://jimmyyu888.com/drive/api` + Bearer token;视频过 Encode Media 分支(顺手转成 H.264);照片/视频/PDF 三类实测全中。**搭建/排障圣经:`pi-upload-shortcuts-guide.md`(网盘根+桌面)**。血泪经验:Shortcuts 的 AI 重建动作必丢 Authorization 头;Header 的 Key 必须填 Authorization、值带 `Bearer ` 前缀;变量顺序不能引用下方动作;批量传需开"允许共享大量数据"。
