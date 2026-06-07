---
name: Daily backup must mirror entire .claude including secrets
description: Daily backup of ~/.claude to GitHub is full-mirror, intentionally includes credentials and API keys
type: feedback
originSessionId: 76134288-12f4-49ff-bf21-2d292ce78d6f
---
The daily backup at 04:00 (Windows Task Scheduler `ClaudeConfigBackup` running `~/.claude-config-git/sync.ps1`, pushing to private repo `Jimmyyu725/Claude-Backup-Windows`) must mirror the **entire** `C:\Users\y3264\.claude` directory. Do NOT add gitignore rules to skip `.credentials.json`, API key files, `projects/`, `plugins/`, `cache/`, etc.

**Why:** User explicitly chose full backup over selective backup ("这些也备份，不要问，做就行了") on 2026-04-27, accepting that the private repo holds tokens and personal data. Earlier selective version missed too much on disaster recovery. User confirmed again with "记住要备份所有的 C:\Users\y3264\.claude 包括apikey".

**How to apply:** When editing `~/.claude-config-git/sync.ps1` or its `.gitignore`, do not narrow scope back. Only the destination repo's own metadata (`.git/`, `sync.ps1`, the repo's own `.gitignore`) is excluded via `robocopy /XD .git /XF sync.ps1 .gitignore`. Embedded `.git` inside skill folders is also skipped so skills track as regular files. Everything else from `.claude/` mirrors over verbatim. Repo MUST stay private.
