# NCCU schedule auto-update workflow

When user mentions ANY change/addition/removal to NCCU exchange schedule items (deadlines, events, milestones, status updates), automatically update BOTH targets without asking for reconfirmation.

## Target 1: MD file
Path: `C:\Users\y3264\Desktop\NCCU\NCCU_Fall2026_Timeline.md`
- Use Edit tool to modify relevant table rows
- For completed items, mark with ✅ prefix in 状态 column
- For new items, add to 主时间线 or 并行任务 section as appropriate

## Target 2: Google Calendar
Tools: `mcp__47805455-0a81-4aac-925f-8fbe1a3510c1__create_event` / `update_event` / `delete_event` (load via ToolSearch if deferred).

Standards:
- Calendar: primary (y326433462@gmail.com)
- Title prefix: `[NCCU]`
- Color: `9` (Blueberry) normal / `11` (Tomato) for high-priority/can't-miss deadlines
- All-day deadlines: `allDay: true`, startTime midnight UTC, endTime next-day midnight UTC
- Description: context + action items + relevant links/contacts

## Existing event IDs (created 2026-05-25)
- `1qgqqbsm1uglc8pcon6pbvq99o` — 7/15 校内宿舍申请截止
- `bl7aih5dqr6ckgv5lil4v4lm1s` — 7/22 OIC 线上 info session(估算)
- `qertdpe19m5s2vpafo5ui1u0jk` — 8/5 NCCU 学号 + Arrival Survey 开放
- `m2njsi0jdnh731seguddpd3br8` — 8/16 校内宿舍取消截止
- `5o1qr1rt3b8ih6v5fgv6j9pd8o` — 8/18 在线选课开始
- `g4efoue59vk7dbc1t5mh0bpm2o` — 8/29 校内宿舍开放入住
- `g5n2rqt3ffdt97urna5so8o32o` — 9/3 OIC Orientation Day
- `h3pautm8pfr30l6sen73lrrpuc` — 9/5 三合一截止(番茄色)
- `7sihshqhbmbfn9k9in82oaubd4` — 9/7 Fall 2026 开课(番茄色)

## Workflow on change
1. Update MD (Edit tool)
2. Update Calendar (create/update/delete_event with stored ID)
3. Briefly report both in response: "MD + Calendar 已同步:<一句话变更摘要>"
4. No reconfirm — execute directly per `feedback_no_reconfirm.md`
