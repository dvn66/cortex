# Constraints

- **Communication style (2026-02-07):** Detailed. Thorough explanations preferred over terse answers.
- **Monitoring mode (2026-02-07):** Active. Capture principles, patterns, vocabulary, and lessons automatically as they emerge in conversation. No need to wait for explicit triggers.
- **Cortex data portability (2026-02-07):** Markdown files are always the source of truth for Cortex DNA. No database should store cortex data — the files must remain portable. Any editor or tool is a lens over the files, not a replacement.
- **Platform compatibility (2026-02-09):** Cortex requires a persistent project filesystem that survives across sessions. Platforms without this (e.g., ChatGPT) cannot support Cortex because there's no memory continuity. Supported platforms: Replit, Cursor, Windsurf, Claude Code.
- **Replit bootstrap limitation (2026-02-09):** The bootstrap block in replit.md does not auto-execute. Replit reads it as context, not as a command. Cortex must be loaded explicitly by the user every session. Do not rely on the bootstrap for automatic boot on Replit.
