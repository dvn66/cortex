# Cortex v2.1

<!-- This file connects your AI agent to Cortex — your persistent memory system. -->
<!-- Do not delete. Your agent reads this at session start. -->

## Instructions for the AI Agent

You have access to Cortex, a persistent memory system that survives session resets.

### First Run (Genesis)

If `cortex/data/` does not exist in this workspace, create it now:

1. Create these directories: `cortex/data/diary/`, `cortex/data/principles/`, `cortex/data/memory/`, `cortex/data/projects/`, `cortex/data/triggers/`, `cortex/data/templates/`, `cortex/data/archive/`
2. Create empty seed files:
   - `cortex/data/principles/goals.md` — `# Goals`
   - `cortex/data/principles/rules.md` — `# Rules`
   - `cortex/data/memory/active.md` — `# Active Memory`
   - `cortex/data/memory/lessons.md` — `# Lessons`
   - `cortex/data/vocabulary.md` — `# Vocabulary`
   - `cortex/data/memory/profile.md` — `# Profile`
   - `cortex/data/memory/considerations.md` — `# Considerations`
3. Copy the trigger definitions from the Triggers section below into `cortex/data/triggers/standard.md`
4. Ask the user: "What's this project about, in a sentence?" — write the answer to `cortex/data/principles/goals.md`
5. Ask: "Should I actively capture principles and patterns as we work, or wait for you to flag them?" — write preference to `cortex/data/principles/rules.md`

### Every Session

1. Read `cortex/data/memory/active.md`, `cortex/data/memory/lessons.md`, `cortex/data/vocabulary.md`
2. Read `cortex/data/memory/profile.md` — calibrate communication to match the user's current level, preferences, and working style. Profile calibrates; it does not constrain.
3. Read all principles files that exist in `cortex/data/principles/` — this includes `goals.md`, `rules.md`, `constraints.md`, and `best-practices.md`. Read whichever are present.
4. Scan `cortex/data/projects/` for files with `Status: active`
5. Read trigger definitions from `cortex/data/triggers/standard.md`. Also read `cortex/data/triggers/local.md` if it exists — these are install-specific triggers.
6. Enter **monitoring mode** — watch all conversation for goals, rules, lessons, vocabulary, and profile self-disclosures. When found, write to the appropriate file in `cortex/data/`. Briefly note what was captured.

### Rules

1. Principles are append-only. Never rewrite without user approval.
2. Diary entries are written during sessions, not reconstructed after.
3. Active memory (`active.md`) gets updated each session. Lessons are append-only.
4. Trigger responses are concise. Action, not explanation.
5. Internal triggers run silently unless the user asks.
6. Monitoring is always on. Capture knowledge as it emerges — including self-disclosures about the user's background, strengths, limitations, or working style (write to `cortex/data/memory/profile.md`).
7. Profile is calibration. Profile facts calibrate how you communicate, what you assume the user knows, and how you frame decisions. Profile does not constrain capability — match the user's current level and adjust as it changes.

### Memory Architecture

- **Principles (RAM):** `cortex/data/principles/` — always loaded. Goals, rules (or constraints + best-practices), lessons. Permanent, append-only.
- **Diary (Disk):** `cortex/data/diary/YYYY/MM/DD.md` — one file per day. Permanent. Only most recent read at session start.
- **Active Memory (Working Set):** `cortex/data/memory/active.md` — where we left off, open issues, next steps. Updated each session.
- **Lessons:** `cortex/data/memory/lessons.md` — patterns learned, failure prevention. Append-only.
- **Vocabulary:** `cortex/data/vocabulary.md` — shorthand, synonyms, project-specific terms.
- **Projects:** `cortex/data/projects/[slug].md` — multi-session missions with tasks and session logs.
- **Considerations (Disk):** `cortex/data/memory/considerations.md` — things connected to our work that might matter later. Stored, not loaded at boot. Searched on demand when relevant context arises.
- **Profile:** `cortex/data/memory/profile.md` — who we're working with. Self-disclosed facts only, never inferred. Living data that updates as the user changes.

## Triggers

When the user types `::code`, read the trigger definition from `cortex/data/triggers/standard.md` (and `local.md` if it exists) and execute it. Any trigger with `?` appended shows brief usage help.

### Trigger Index

| Code | Purpose | Payload |
|------|---------|---------|
| `::ss` | Session start — full briefing, load principles | No |
| `::se` | Session end — diary, projects, memory sync | No |
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
