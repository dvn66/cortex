# Vocabulary

## Cortex Terms

- **DNA** — The two portable files (cortex.md + README.md) that define the entire Cortex system. Carrying these two files to any project and running genesis births a new Cortex instance.
- **Data layer** — The `data/` directory created by genesis. Contains all memories: diary, principles, active memory, lessons, projects, vocabulary, templates, releases, and archive. Unique to each install; not portable.
- **CORTEX_ROOT** — The directory containing cortex.md. All paths in Cortex are resolved relative to this. Auto-detected at boot and during genesis.
- **Genesis** — The birth protocol. Five phases plus optional Deep Seeding: Confirm & Create, Interview, Consent-to-Scan, Deep Seeding (optional), Self-Test, First Diary Entry. Creates the data layer and configures the system for a new project.
- **Deep Seeding** — Optional genesis phase (3b) where the agent reads discovered documentation and code conventions, then suggests initial principles, vocabulary, and lessons to seed the data layer. Requires its own explicit permission gate. Nothing is written without user approval.
- **Boot** — Loading the system into an active state. Reads cortex.md, active memory, vocabulary, local triggers, and scans for active projects. Activates monitoring mode.
- **Monitoring mode** — The default operational state after boot. The agent passively watches all conversation for extractable knowledge (principles, patterns, lessons, vocabulary) and captures it to the data layer in real time.
- **Bootstrap** — The hook in the platform's agent context file (e.g., replit.md) that tells the agent to read cortex.md on startup. Platform-specific file, platform-agnostic content.
- **Trigger** — A `::code` command that invokes system behavior. User triggers are typed explicitly; internal triggers fire automatically as part of agent workflow.
- **RAM (Principles)** — The memory tier that is always loaded into context. Goals, constraints, and best practices. Dense, distilled, actionable. Append-only — never aged out or archived.
- **Disk (Diary)** — The permanent narrative record. One file per day. Searched on demand, not loaded into every session. Never compressed or deleted.
- **Working set (Active Memory)** — Short-term memory: current state, open issues, where we left off. Subject to aging (Hot/Warm/Cold/Archived).
- **Memory aging** — The protocol that governs active memory lifecycle. Hot (last 3 sessions), Warm (5-10 sessions), Cold (10+ sessions), Archived (moved to data/archive/).
- **Shepherd behavior** — The agent's responsibility to track active projects across sessions and nudge the user about unfinished work at boot and session start. Projects are first-class memory citizens.
- **Append-only** — The write policy for principles and lessons. New entries are added; existing entries are never rewritten or removed without explicit user approval.
- **Atomic writes** — The file write strategy used by cortex-writer.ts. Creates a .bak backup before every write to prevent data loss from interrupted operations.
- **Round-trip fidelity** — The guarantee that reading a markdown file, parsing it, editing it, and writing it back preserves all content that wasn't intentionally changed.
- **Local triggers** — Install-specific trigger extensions stored in `data/triggers/local.md`. They don't travel with the DNA. Loaded at boot, listed in `::?` with a `[local]` tag.
- **Diary consolidation** — The protocol for managing diary volume over time. After 60 days, a calendar month's daily entries are eligible to be compressed into a single monthly summary. Originals are archived, never deleted. Requires human approval.
- **genesis-seeded** — Tag applied to data layer items that were created during the optional Deep Seeding phase of genesis. Distinguishes items extracted from pre-existing documentation from those captured organically during sessions.
- **CoVe (Chain of Verification)** — A technique for reducing AI hallucination by decomposing claims into verification questions, answering independently, then revising. Noted as a candidate for future Cortex workflows.

## Project Terms

- **X CMS** — The content management system for the @cortex_agent X (Twitter) account. Compose posts/threads, schedule, manage status workflow (draft/scheduled/posted), copy-to-clipboard for manual posting.
- **DNA Editor** — The visual interface for reading and editing Cortex DNA through the app. Seven pages: Overview, Triggers, Principles, Memory, Projects, Templates, Releases. All edits round-trip to markdown files.
- **Two-pillar system** — The app's architecture: X CMS (content management) + Cortex DNA Editor (memory management). Established when the DNA Editor was added as the second major feature set.
- **cortex-parser.ts** — Server-side module that reads and parses all cortex markdown files into structured data for the API. Handles triggers, principles, overview stats, memory, projects, templates, and releases.
- **cortex-writer.ts** — Server-side module that writes changes back to cortex markdown files. Includes path traversal prevention, .bak backups, and atomic write strategy.
- **Interface Contract Registry** — The PRD convention requiring every API boundary to have exact TypeScript request/response shapes defined. No "TBD" or undefined types allowed.
- **Phase-gated implementation** — The development approach used for the DNA Editor: build one phase, pause for review, then proceed. Four phases total.
- **Seam failure** — Bugs that occur at the boundary between two systems or components (e.g., parser output not matching API contract). The interface contract registry was designed to prevent these.

## Shorthand

- **::ss** — Session start
- **::se** — Session end
- **::n** — Quick note to diary
- **::d** — Write diary narrative
- **::p** — Add a principle
- **::r** — Review all principles
- **::m** — Show active memory
- **::proj** — Project management
- **::nt** — Create new trigger
- **::wtf** — Diagnostic ("something went wrong")
- **::boot** — Load system
- **::?** — List all triggers
- **::release** — Create versioned release (local trigger)
- **::releases** — List all releases (local trigger)
- **::ingest** — Absorb recent context into knowledge
- **::verbatim** — Raw copy of recent exchange(s)
