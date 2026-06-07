---
name: Never expose the OpenAI API key
description: API key has leaked twice — never print/echo its value anywhere; only test presence
type: feedback
originSessionId: 66fecf23-7c3c-4152-b96e-250a7d00a199
---
Never print, echo, log, or otherwise surface the value of `OPENAI_API_KEY` (or any secret) in chat, command output, or files.

**Why:** The key has already been leaked **twice** in this project via PowerShell/chat output. The user is highly security-sensitive about this; a third leak would mean another key rotation and lost trust.

**How to apply:**
- To check the key exists, only test the boolean: `if ($env:OPENAI_API_KEY) {...}` or `[bool][Environment]::GetEnvironmentVariable("OPENAI_API_KEY","User")`. Never write a command that would expand/display the value.
- Load it without echoing: `$env:OPENAI_API_KEY = [Environment]::GetEnvironmentVariable("OPENAI_API_KEY","User")`.
- PowerShell escape character is backtick `` ` ``, NOT backslash `\` — relevant when quoting in commands near the key.
- Applies cross-cutting, not just this project: treat any user secret the same way.
