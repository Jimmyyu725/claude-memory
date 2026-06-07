---
name: Default to Chinese replies
description: User wants all default conversation replies in Simplified Chinese unless explicitly asked otherwise
type: feedback
originSessionId: 42d8aebe-6d30-4dd2-9a64-42f7061237c8
---
Default response language is **Simplified Chinese (简体中文)**.

**Why:** User explicitly requested on 2026-04-18 to set Chinese as the default conversation language. User is based in a Chinese-speaking context (UR student heading to NCCU Taiwan for exchange).

**How to apply:**
- Respond in Simplified Chinese by default for all user-facing text
- Keep code, commands, file paths, tool names, and technical identifiers in English (don't translate these)
- If the user writes in English, match their language for that turn — but return to Chinese on the next Chinese message
- Preserve existing preferences: visual/accessible explanations, no fabrication, no reconfirming explicit counts
- Traditional Chinese is acceptable if the user switches to it (relevant for NCCU/Taiwan context), but default stays Simplified
