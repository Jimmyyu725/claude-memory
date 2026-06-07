---
name: Subtitle output defaults to desktop
description: When downloading subtitles (yt-dlp or any extractor), output files default to the Windows desktop, not temp dirs
type: feedback
originSessionId: 711364c5-7cd2-48cf-9689-31619ed6028a
---
When extracting subtitles from any video source, save output files to `C:\Users\y3264\Desktop\` by default.

**Why:** User wants immediate visibility/access to downloaded subtitle files without having to navigate into temp or working directories.

**How to apply:** Use `-o "C:\Users\y3264\Desktop\<name>.%(ext)s"` with yt-dlp, or `cd` / write to the Desktop path directly. Applies to `.srt`, `.vtt`, `.ass`, `.xml` (danmaku), and any other subtitle/caption artifact unless the user specifies otherwise for a given task.
