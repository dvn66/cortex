# Cortex

Persistent memory for AI coding agents. One file, any platform, zero dependencies.

## The Problem

AI coding agents start every session with amnesia. They re-read your codebase, re-learn your conventions, re-discover your decisions, and re-make mistakes you already corrected. The longer your project runs, the more expensive this gets — in tokens, in time, and in frustration.

## What Cortex Does

Cortex gives your agent a structured memory system that survives session resets. It captures principles, lessons, patterns, and vocabulary as you work — so your next session starts where the last one ended, not from scratch.

- **Principles (RAM):** Design decisions, constraints, and best practices — always loaded, always in context
- **Diary (Disk):** Narrative record of each session — permanent, searchable, never bulk-loaded
- **Active Memory (Working Set):** Where you left off, open issues, next steps — ages naturally over time
- **Projects:** Multi-session missions with task tracking — the agent shepherds them to completion across sessions
- **Concept Dictionary:** Shared vocabulary that eliminates re-explanation of established patterns

## How It Works

Cortex is one file: **cortex.md** — the operating manual. It contains everything an AI agent needs to birth, boot, and run a persistent memory system. Trigger definitions, memory architecture, behavioral rules, genesis protocol — all in one portable markdown file.

No database. No API keys. No build step. No vendor lock-in. Just a file your agent reads and writes.

## Quick Start

**Option 1 — Upload the file:**
1. Download `cortex.md` from this repo
2. Upload it to your project
3. Tell your agent: "Read and act on cortex.md"
4. Type `::genesis`

**Option 2 — Paste this into chat** (for platforms that don't support .md uploads):
```
Fetch https://raw.githubusercontent.com/dvn66/cortex/main/cortex.md, save it to this project, read it, and run ::genesis
```

Genesis runs a short interview (3 questions), scans your project (with permission), and creates the data layer. Takes about 2 minutes.

## After Genesis

```
::boot     — Load the system (start of any session)
::ss       — Full session briefing (principles + recent diary + active projects)
::se       — End session (write diary, update memory, flag stale items)
::?        — List all triggers
```

The agent enters **monitoring mode** after boot — it passively captures principles, vocabulary, and lessons as they emerge in conversation. You don't have to explicitly tell it to remember things.

## Platform Compatibility

Cortex works with any AI coding assistant that reads a context file. Genesis auto-detects your platform and writes the bootstrap hook to the right file.

**Last updated:** 2026-02-09 | **Cortex version:** v1.5.0

### Test Categories

| Code | Test | What it validates |
|------|------|-------------------|
| T1 | Genesis | Data layer creation, platform detection, interview, self-test |
| T2 | Boot | System loads, reads memory, enters monitoring mode |
| T3 | Triggers | Core triggers fire correctly |
| T4 | Persistence | Files written during session readable in next session |
| T5 | Continuity | Session end then session start restores context |
| T6 | Monitoring | Passive capture of principles/vocabulary during conversation |

### Results

| Platform | Type | Context File | T1 | T2 | T3 | T4 | T5 | T6 | Verdict |
|----------|------|-------------|----|----|----|----|----|----|---------|
| Replit | Cloud IDE | `replit.md` | -- | -- | -- | -- | -- | -- | -- |
| Cursor | Desktop IDE | `.cursorrules` | -- | -- | -- | -- | -- | -- | -- |
| Windsurf | Desktop IDE | `.windsurfrules` | -- | -- | -- | -- | -- | -- | -- |
| Claude Code | Terminal CLI | `CLAUDE.md` | -- | -- | -- | -- | -- | -- | -- |
| Bolt.new | Cloud | TBD | -- | -- | -- | -- | -- | -- | -- |
| Lovable | Cloud | TBD | -- | -- | -- | -- | -- | -- | -- |
| v0 | Cloud | TBD | -- | -- | -- | -- | -- | -- | -- |
| VibeCodeApp | Mobile/Web | TBD | -- | -- | -- | -- | -- | -- | -- |
| Cline | VS Code ext | TBD | -- | -- | -- | -- | -- | -- | -- |
| Aider | Terminal CLI | TBD | -- | -- | -- | -- | -- | -- | -- |

**Scoring:** Pass / Partial (works with workaround) / Fail / N/A / -- (not yet tested)
**Verdict:** Compatible (T1-T6 all Pass/Partial) | Usable (T1-T4 Pass/Partial) | Incompatible (T1 or T2 Fail)

Full platform profiles and research: see `docs/prd-agentic-platform-landscape.md`.

## Why Not Just Use a Long System Prompt?

System prompts don't learn. They're static. Cortex is living — it grows with your project:

- **Cheaper over time:** Each session boots from ~40 lines of active memory + ~100 concept entries instead of re-reading thousands of lines of source code
- **Targeted retrieval:** Historical context searched on demand, not bulk-loaded into every session
- **Shared language:** Once a pattern is named in the concept dictionary, it never needs re-explaining
- **Fewer false starts:** Principles and lessons prevent the agent from re-proposing approaches you already rejected
- **Self-correcting:** Internal diagnostics detect when the agent has drifted from protocol

## What Cortex Creates

After genesis, Cortex creates a `data/` directory alongside cortex.md:

```
data/
├── diary/          ← Session narratives (permanent record)
├── principles/     ← Goals, constraints, best practices (always loaded)
├── memory/         ← Active working set + lessons learned
├── projects/       ← Multi-session mission tracking
└── vocabulary.md   ← Concept dictionary (shared language)
```

The `data/` directory is yours — project-specific, never committed back to this repo.

## Triggers at a Glance

| Trigger | Purpose |
|---------|---------|
| `::boot` | Load system, orient to current state |
| `::ss` | Session start — full briefing |
| `::se` | Session end — write diary, update memory |
| `::d` | Write today's diary narrative |
| `::n text` | Quick note to today's diary |
| `::p text` | Add a principle |
| `::r` | Review all principles |
| `::m` | Show active memory |
| `::proj` | List/create/manage multi-session projects |
| `::ingest` | Absorb recent context into permanent knowledge |
| `::verbatim` | Raw copy of recent exchanges |
| `::update` | Check for and apply DNA updates |
| `::?` | Show all triggers |

## License

MIT — use it however you want.

## Contributing

Cortex is early. If you're using it with an AI coding assistant and have improvements to the trigger system, memory architecture, or genesis protocol, open an issue or PR. The DNA should stay platform-agnostic — project-specific customizations belong in your project, not here.
