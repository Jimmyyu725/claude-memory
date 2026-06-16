# Memory Index

## 关于我本人

- [User profile](user_profile.md) — 于京田/Jimmy Yu, **US citizen**, U **Richmond**(≠Rochester) BSBA Finance; prefers visual explanations over jargon
- [NCCU exchange](user_nccu_exchange.md) — UR sophomore, Fall 2026 exchange to NCCU Taiwan, College of Commerce
- [User English level: 9035 词目 (C1+/近 C2)](user_english_level.md) — 墨墨实测;盲点是常见词的少见词义(如 felt=毛毡)
- [UR Finance switch](project_ur_finance_switch.md) — 转金融方向(原 Marketing),目标 2028 春毕业;NCCU 交换最多只能转 1 门金融选修,校外学分要选非商学院课

## 我定下的规则

- [Default language Chinese](feedback_language_chinese.md) — reply in Simplified Chinese by default; keep code/paths/tool names in English
- [Code & docs in English only](feedback_code_english_only.md) — **死规矩**:所有代码/注释/字符串/commit/Markdown 文档一律地道英文;只有对话回复可中文
- [No reconfirm on explicit counts](feedback_no_reconfirm.md) — when user gives a number or "all", execute; don't narrow or reconfirm
- [Don't fabricate facts](feedback_no_fabrication.md) — never state speculation as fact; verify or explicitly flag as guess; user has caught this twice
- [Never expose the OpenAI API key](feedback_api_key_security.md) — key leaked 2×; only test presence, never print value
- [Full-mirror .claude backup](feedback_backup_full_claude_dir.md) — daily 04:00 backup must include EVERYTHING (credentials, projects, plugins, API keys); don't narrow scope
- [Subtitles → Desktop](feedback_subtitle_output_desktop.md) — downloaded subtitles default to `C:\Users\y3264\Desktop\`, not temp dirs
- [Vocab confusion file auto-append](feedback_vocab_confusion_autoupdate.md) — 用户每问"A vs B",自动追加到桌面 `英语易混词辨析.md`,模板固定
- [NCCU schedule auto-update](feedback_nccu_schedule_autoupdate.md) — 任何 NCCU 时间表变动,自动同步更新 MD 文件 + Google Calendar([NCCU] 前缀,蓝莓=普通/番茄=高优)
- [项目代码统一存放](feedback_project_code_location.md) — `C:\Project` 是默认/兜底落点(短名子文件夹);Unity 等有自己工程目录的程序用其默认位置、Claude Code 配置、用户指定路径除外
- [工作流子 agent 联网会被拒](feedback_workflow_subagent_tools.md) — 后台自主模式下子 agent 的 WebSearch/WebFetch 会被自动拒绝而卡死;联网核验在主线程做,子 agent 只派只读任务
- [浏览器自动化默认走 9222](feedback_browser_via_cdp_9222.md) — 任何浏览器自动化/搜索连常驻 chrome-cdp(127.0.0.1:9222),不新开 Chrome;要登录态用默认上下文,不可信浏览用隔离 incognito 上下文用完即关

## 项目与参考

- [DoomFollow 游戏](project_doomfollow_game.md) — 《末日追随》2D 横版僵尸射击(C#/MonoGame,不用 Unity),在 `C:\Project\DoomFollow`
- [GalGang Unity 工程 + Unity MCP](project_galgang_unity_mcp.md) — F:\ 上的 Unity 6 项目,已接 Claude Code(unity-mcp/relay 操控编辑器,需重启生效)
- [gpt-image 透明背景](reference_gpt_image_transparency.md) — gpt-image-2 不支持透明,精灵图用 gpt-image-1.5
- [CCGS 全局安装](reference_ccgs_global_install.md) — Claude-Code-Game-Studios 的 73 skill+49 agent 已装到 ~/.claude;改名 ccgs-code-review/ccgs-help
- [MiroFish 预测引擎](project_mirofish.md) — 多智能体群体模拟,在 `C:\Project\MiroFish`,配 OpenAI gpt-4o-mini + Zep,前后端已跑通
- [GesturePlay 手势插件](project_gesture_seek.md) — 摄像头手势控 YT/B站(捏合拖进度+握拳播放暂停),在 `C:\Project\GestureSeek`(夹名故意未改),v1.0.0 上架就绪;repo=Jimmyyu725/GesturePlay
- [API key 存放位置](reference_api_keys_env_local.md) — 用户的 key 放在 `C:\Users\y3264\.env.local`,从那读、别让他贴明文
- [VLESS 私人代理](project_vless_proxy.md) — 自建 Vultr 东京 VLESS+Reality;Win 用 v2rayN;备忘在桌面(含密钥,敏感)
- [Jimmy Drive 自研网盘+门户](project_jimmy_drive.md) — `C:\Project\JimmyDrive`;drive.jimmyyu888.com + 玻璃门户;Quantum API 硬经验(isDir/静默覆盖/SessionId)全在这;**JimmyDrive/GestureSeek commit 后必 push 自家 Gitea(https://git.jimmyyu888.com)**
- [RC 飙速车(当前主项目)](project_rc_speedcar.md) — 2026夏动手主项目;1/10 触地车散件自装,目标60-80km/h,~$280,在 `C:\Project\RC-SpeedCar`
- [Pi 4 自建小服务器](project_pihole.md) — 原计划Pi-hole已改向;CanaKit Pi4 2GB套件($145,6/6到货)做Docker家庭服务器(Vaultwarden/Gitea/Tailscale等),在 `C:\Project\PiServer`;**U盘已LUKS+Adiantum加密,钥匙绑SoC序列号,救命材料在 .env.local + PiBackup\**;Pi时钟=UTC-5
- [于京田百科](project_jimmy_encyclopedia.md) — 关于用户本人的自托管个人维基(18词条,SilverBullet/notes.jimmyyu888.com),证据=盘+Chrome史+Steam+记忆;repo `C:\Project\JimmyWiki`;含完整画像速记
- [ClaudeWeb 网页版 Claude Code](project_claudeweb.md) — **已下线 2026-06-11**(从未启用,改用 CLI);repo 保留;合规结论:无头只能 API key,订阅违反 Consumer §3.7
- [Claude Console 会话管理器](project_claude_console.md) — **2026-06-15 自建**;code.jimmyyu888.com 上 ttyd 前的会话列表页(进入/暂停/删除/远程控制 tmux 会话);Pause=cgroup freezer(SIGSTOP 会被 tmux 复活);后端 `claude-console.service`:7682
- [邮箱别名方案](reference_email_alias.md) — 自有域名 `jimmyyu888.com`(Cloudflare)做 catch-all,`任意@jimmyyu888.com`→转发到 Gmail;只收不发,双向对话用 DuckDuckGo
- [记忆 git 同步](reference_memory_git_sync.md) — 记忆同步到 GitHub **private** 库 `Jimmyyu725/claude-memory`(含敏感信息,永久 private);两台 Pi 已退役,现由 jimmynas 维护;token 受 sudo 墙阻挡,改用登录态浏览器网页上传同步
