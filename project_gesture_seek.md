---
name: project-gesture-seek
description: GesturePlay(原名 GestureSeek)—— 摄像头手势控制 YouTube/B站 的 Chrome 扩展(捏合拖进度、握拳播放/暂停)
metadata: 
  node_type: memory
  type: project
  originSessionId: 85be0f6f-52ce-425c-8880-034f2c4eea1f
---

**GesturePlay**(2026-06-10 由 GestureSeek 改名,用户定名,查重无撞车;v1.0.0 为上架就绪版):用 USB 摄像头识别捏合手势(👌)+ 水平移动手,在 YouTube 和 Bilibili 上像拖真进度条一样实时拖动视频进度;握拳切换播放/暂停。在 `C:\Project\GestureSeek`(**文件夹故意保留旧名**——改路径会换未打包扩展的 ID,导致摄像头授权与 storage 命名空间作废)。GitHub 仓库已改名 `https://github.com/Jimmyyu725/GesturePlay`(旧 URL 自动重定向),ZIP=`dist/GesturePlay-v1.0.0.zip`。内部标识(`gs*` 键、`gs-*` 消息)未改。商店素材:`assets/store/` 两张 1280×800 截图(AI 手势插画 gpt-image-1.5 + HTML 排版 + 无头 Edge 渲染,管线在 `tools/`)。

经 brainstorm 确认的核心交互:
- 手势:捏合 = 抓进度条,松开 = 放下;实时拖动(画面跟手跳)
- 映射:满屏宽度 = 整条视频(按总长比例),相对锚定(捏的瞬间不跳)
- 镜像翻转:手往用户右侧 = 视频前进
- 摄像头:进 YT/B站标签页即自动开;离开即停
- 不加额外 UI,靠原生进度条反馈

架构(Manifest V3,纯前端):offscreen 文档跑 getUserMedia + MediaPipe HandLandmarker(本地模型,绕开网站 CSP)→ service worker 中枢 → content script 改 `<video>.currentTime`。

设计文档:`docs/superpowers/specs/2026-06-07-gesture-seek-design.md`。

2026-06-07:用户授权全自主开发(≥10 agent 并行,做完才汇报),用户最终只需"加载已解压扩展"安装。

**已完成(2026-06-07,当前 v0.3.0,已 git 提交)**:全部代码写完,26 个状态机单测通过,经多轮 agent 对抗式审查并修复。装法:Chrome `chrome://extensions` → 开发者模式 → 加载已解压 → 选 `C:\Project\GestureSeek`。首次在 YT/B站视频页点"允许"摄像头。**改代码后用户要在 chrome://extensions 点该扩展的刷新图标 + 刷新视频页**才生效。
- v0.2/0.3 据用户反馈加了:暂停修复(自适应节流+松手精确落点);全屏修复(根因=camera.js 的 rAF 在 iframe 不被绘制时暂停 → 改 setTimeout 定时器,iframe 固定挂 body 不再重挂)。
- v0.4 用户要"用网站原生进度条而非自定义浮层":删掉自定义浮层,改 currentTime 让原生红条跟着走 + 拖动时合成 mousemove 让原生控制条显示。还加了过滤 MediaPipe 两条无害 console.warn 噪音(`OpenGL error checking`/`NORM_RECT`),并提醒 chrome://extensions 错误面板会累积、需手动"全部清除"。
- 商店上架准备(2026-06-10):**未上传**(需用户本人 $5 开发者账号 + 控制台操作)。已备齐:`tools/pack.ps1` 出干净 ZIP(9.4MB,剔除 nosimd/module wasm 与备用模型)→ `dist/`;`PRIVACY.md`;`docs/store-listing.md`(中英文案+隐私表答案+提交步骤)。剩余:注册账号、传 ZIP、贴文案、截图≥1 张 1280×800、隐私政策 URL 需公开可访问(仓库转 public 或 Gist)、选 Unlisted/Public、提交审核(数天)。
- v0.9:**默认精细拖动**——整幅手扫过 = `gsRange` 秒(默认 60,封顶视频长度),设置页下拉可选 30s/1m/2m/5m/整条视频(=旧比例行为);gesture-core 自身默认 `rangeSec:0` 保持向后兼容,产品默认放 content.js。
- v0.6–0.8:设置弹窗(滑块实时调 死区/握拳时长/手指数/捏合灵敏度)+ 可选摄像头骨架预览;中英双语 UI(`i18n.js`,en/zh 键对齐,CI 校验);**全项目英文化**;**已推 GitHub(私有)`https://github.com/Jimmyyu725/GestureSeek`**,main 分支,GitHub Actions CI(测试+语法+manifest+i18n parity)已绿;MIT LICENSE。v0.8:总开关 `gsEnabled`、握拳计时改毫秒 `holdMs`(修 30fps 假设 bug)、设置迁到 `chrome.storage.sync` 跨设备漫游(滑块写入防抖 200ms 避配额)。Mac 可用(clone + 加载已解压 + 系统设置允许 Chrome 摄像头)。
- v0.5:✊**握拳保持约半秒 = 切换播放/暂停**(边沿触发+去抖+拖动中屏蔽),张开=休息位。同时修了"握拳被误判成捏合去拖进度"的 bug。引擎从 HandLandmarker 换成 **GestureRecognizer**(`gesture_recognizer.task`,本地,握拳=`Closed_Fist` 标签);捏合仍用关键点算。camera.js 顶部 `ENGINE` 常量可切回 HandLandmarker(`hand_landmarker.task` 保留)。MediaPipe 跑在 **GPU**(WebGL),CPU 兜底。39 个单测,经 6-lens agent 审查 0 blocker。
- 关键教训:**工作流子 agent 的联网工具(WebSearch/WebFetch)在后台自主模式会被权限自动拒绝而卡死**;只读子 agent(Read/Grep/Glob)正常。联网核验要在主线程做。见 [[feedback-workflow-subagent-tools]]。
- 关键技术坑:**MV3 offscreen 文档开不了摄像头**(隐藏页无法授权),必须用注入页面的扩展源 iframe + `allow="camera"`(既能授权又受扩展 CSP 允许 wasm)。
