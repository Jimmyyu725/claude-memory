---
name: No reconfirm on explicit counts
description: When user gives a number or "all", execute directly; don't narrow scope or ask for re-confirmation
type: feedback
originSessionId: 1d27515e-7b1f-4024-a15a-aff739f1cd1b
---
When the user gives an explicit count (e.g., "3", "5", "10") or a total like "all" / "全部" / "每个", just execute at that scope. Do not narrow it to a smaller subset, and do not ask "are you sure you want all X?"

**Why:** User finds it annoying when I second-guess explicit instructions they already gave clearly. Asking "just to confirm, you want all of them?" wastes their time when they already said so.

**How to apply:**
- "全部" / "all" / "每个" → do all of them, not a sample
- Specific number ("给我 10 个") → give exactly that many, not 3 with "let me know if you want more"
- Do NOT preemptively narrow: if they say "处理所有文件", process all, don't offer "I'll start with the first 5"
- Do NOT ask "really all?" / "确定全部吗？" — they already said so

**Note:** This file was reconstructed on 2026-04-17 from the MEMORY.md index hook after the original was lost. If the reconstruction misses nuance from the original, user should correct.
