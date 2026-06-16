---
name: project_jimmy_encyclopedia
description: "《于京田百科》——关于用户本人的自托管个人维基,在 SilverBullet/notes.jimmyyu888.com,repo C:\\Project\\JimmyWiki"
metadata: 
  node_type: memory
  type: project
  originSessionId: f978d678-1afc-474c-9ab6-9a8bc64f9c32
---

**The Jimmy Yu Encyclopedia(2026-06-11 一夜建成)**:用户要求"造一部关于我自己的百科,时间地点人物兴趣全分析到位",并明确要"多 agent 处理、开始后别问问题、干到完工"。我用证据驱动 + 18-agent 工作流做成,落在他自己的 **SilverBullet 个人维基**。

- **成品**:18 个词条(17 分页 + 主页 index),英文撰写(遵守"Markdown 文档英文"死规矩),互相 `[[双链]]`。词条:Profile / Academics / NCCU Exchange / Finance & Investing / Homelab / Software Projects / AI Tooling / Gaming / Football / Music & Film / Cosmology & Curiosity / Hobbies & Lifestyle / Places & Travel / Timeline / Daily Rhythm & Devices / Digital Footprint / Methodology & Sources。
- **在哪**:SilverBullet 空间 `/srv/fileshare/Notes/*.md`(加密盘上),`https://notes.jimmyyu888.com` 登录后浏览(index 即主页)。源码 repo `C:\Project\JimmyWiki`,已推自家 Gitea(`jimmy/JimmyWiki`,private)。
- **证据源**(全本机、已授权,采集脚本在 repo `_evidence/`,**已 gitignore**——含浏览历史/全路径,敏感):全盘清单 101 万文件(`inventory.txt`);Chrome 历史 27749 URL+300 搜索词,窗口 **2026-02-28..05-22**(`history_chrome.txt`,Python 读 SQLite 副本);Steam 47 装机+173 时长(`steam_leaderboard_named.txt`,appid 经 store appdetails 精确解析);长期记忆。全部固化进 `_evidence/DIGEST.md` 作引用底本。
- **铁律(都执行了)**:零编造(每条非显然事实标来源,推测标置信度,无据留白);零密钥(部署前跑正则扫描 `682850/cfut_/sk-/AAAA/FILESHARE_LUKS/40+位hex`,clean;一款成人游戏从 Steam 列表里悄悄略去);英文。
- **画像速记**(供以后参考):US citizen;家在 **Lake Forest, IL**(芝加哥郊区,IL 驾照);UR 金融(原 Marketing,目标 2028 春);**夜猫子**;重度大战略玩家(文明6 189h、FM23 118h、Stellaris/Victoria3/CK3/EU4/HOI4);足球迷(世界杯2026抢票、FM、曼城);宇宙学好奇;Whoop 健身;Mercedes/Forza;Umarex 气枪;aespa(Winter)/周杰伦;装备 9950X3D+4080 台式 + M3 Pro Mac。
- **怎么刷新**:重跑 `_evidence/` 里的 `extract_history.py`+`extract_steam.py`+`resolve_top_games.py`+inventory,更新 DIGEST,再跑工作流(脚本 `jimmy-encyclopedia`),`parse_pages.py` 写盘,curl 批量传到 `/Notes/`。
- 关联 [[project_pihole]](宿主)、[[project_jimmy_drive]](同盘网盘)、[[feedback_no_fabrication]]、[[api-keys-env-local]]。
