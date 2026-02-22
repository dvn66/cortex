# Cortex v2.2

<!-- This file connects your AI agent to Cortex — your persistent memory system. -->
<!-- Do not delete. Your agent reads this at session start. -->

## Instructions for the AI Agent

You have access to Cortex, a persistent memory system that survives session resets.

### First Run (Genesis)

If `cortex/data/` does not exist in this workspace, create it now:

1. Create these directories: `cortex/data/system/`, `cortex/data/diary/`, `cortex/data/principles/`, `cortex/data/memory/`, `cortex/data/projects/`, `cortex/data/triggers/`, `cortex/data/templates/`, `cortex/data/archive/`
2. Fetch the seed manifest from `https://raw.githubusercontent.com/dvn66/cortex/main/seed-manifest.json` and create all files listed in it. If fetch fails, ask the user to paste the seed manifest content.
3. After seeding, read `cortex/data/system/genesis.md` and execute the interview steps (project context, working style preference).
4. Write the first diary entry recording the genesis.

### Every Session

1. Read `cortex/data/system/rules.md` — these are your operating rules.
2. Read `cortex/data/system/architecture.md` — understand the memory tiers.
3. Read `cortex/data/memory/active.md`, `cortex/data/memory/lessons.md`, `cortex/data/vocabulary.md`.
4. Read `cortex/data/memory/profile.md` if it exists — calibrate communication to match the user's level and working style. Profile calibrates; it does not constrain.
5. Read all files in `cortex/data/principles/` — goals and rules. Read whichever are present.
6. Scan `cortex/data/projects/` for files with `Status: active`.
7. Read trigger definitions from `cortex/data/triggers/standard.md`. Also read `cortex/data/triggers/custom.md` if it exists.
8. Enter **monitoring mode** — watch all conversation for goals, rules, lessons, vocabulary, and profile self-disclosures. When found, write to the appropriate file in `cortex/data/`. Briefly note what was captured.

### Rules

1. Principles are append-only. Never rewrite without user approval.
2. Diary entries are written during sessions, not reconstructed after.
3. Active memory (`active.md`) gets updated each session. Lessons are append-only.
4. Trigger responses are concise. Action, not explanation.
5. Internal triggers run silently unless the user asks.
6. Monitoring is always on. Capture knowledge as it emerges — including self-disclosures about the user's background, strengths, limitations, or working style (write to `cortex/data/memory/profile.md`).
7. Profile is calibration. Profile facts calibrate how you communicate, what you assume the user knows, and how you frame decisions. Profile does not constrain capability — match the user's current level and adjust as it changes.

### Memory Architecture

- **Principles (RAM):** `cortex/data/principles/` — always loaded. Goals and rules. Permanent, append-only.
- **Diary (Disk):** `cortex/data/diary/YYYY/MM/DD.md` — one file per day. Permanent. Only most recent read at session start.
- **Active Memory (Working Set):** `cortex/data/memory/active.md` — where we left off, open issues, next steps. Updated each session.
- **Lessons:** `cortex/data/memory/lessons.md` — patterns learned, failure prevention. Append-only.
- **Vocabulary:** `cortex/data/vocabulary.md` — shorthand, synonyms, project-specific terms.
- **Projects:** `cortex/data/projects/[slug].md` — multi-session missions with tasks and session logs.
- **Considerations (Disk):** `cortex/data/memory/considerations.md` — things connected to our work that might matter later. Stored, not loaded at boot. Searched on demand when relevant context arises.
- **Profile:** `cortex/data/memory/profile.md` — who we're working with. Self-disclosed facts only, never inferred. Living data that updates as the user changes.

## Triggers

When the user types `::code`, read the trigger definition from `cortex/data/triggers/standard.md` (or `custom.md`) and execute it. Any trigger with `?` appended shows brief usage help.

### Trigger Index

| Code | Purpose | Payload |
|------|---------|---------|
| `::ss` | Session start — full briefing, run ::lt, activate monitoring | No |
| `::se` | Session end — diary, projects, memory sync | No |
| `::lt` | Live test — health check, verify Cortex integrity | No |
| `::?` | List all triggers | No |
| `::n` | Capture a note to diary | Yes: text |
| `::d` | Write diary narrative | No |
| `::r` | Review all principles, lessons, memory | No |
| `::ingest` | Capture knowledge (with text or from context) | Optional |
| `::proj` | Current project — tasks, status, notes | Optional |
| `::verbatim` | Copy last N exchanges raw | Optional: count |
| `::wtf` | Diagnostic — something went wrong | Yes: description |
| `::uninstall` | Remove Cortex (preserves data) | No |
| `::nt` | Create a new custom trigger | Yes: code + purpose |

Alias: `::p` works the same as `::ingest`. `::nt?` shows how to create a trigger.

### Internal Triggers (automatic, silent)

- **after-task-complete** — Scan completed work for principles to capture
- **after-bug-fix** — Capture failure pattern to lessons
- **pre-work** — Load principles before significant implementation
- **vocabulary-capture** — Capture terms/shorthand from conversation

## Cloud Sync (Optional)

All storage is local to this workspace. To sync memory across workspaces: visit cortexmem.dev/connect
