# Cortex v1.0.0

## System Definition

Cortex is a collaborative memory system between a human and an AI agent. It persists across session resets. The portable DNA is two files: **README.md** (how — the quick-start) and **cortex.md** (what — this file, the full operating manual). A third file, **vision.md**, is generated during genesis — not carried. This file is the DNA. Everything needed to birth, boot, and run Cortex is here.

## Location & Directory Structure

Cortex is location-agnostic. Drop the DNA files anywhere in a project. The directory containing cortex.md becomes **CORTEX_ROOT**. Genesis creates everything else relative to CORTEX_ROOT.

```
CORTEX_ROOT/                   ← Wherever cortex.md lands (auto-detected)
├── README.md                  ← How. Quick-start guide. Carried with the DNA.
├── cortex.md                  ← What. This file. The full operating manual (the DNA).
└── data/                      ← Created by genesis, sibling to cortex.md
    ├── vision.md              ← Why. Generated during genesis from interview answers.
    ├── what-is-cortex.md      ← Full explainer (created on birth)
    ├── birth-story.md         ← Origin narrative (created on birth)
    ├── transcript.md          ← Design conversation record
    ├── diary/
    │   └── YYYY/
    │       └── MM/
    │           └── DD.md      ← One file per day
    ├── principles/
    │   ├── goals.md           ← What we're building and why
    │   ├── constraints.md     ← Dos and don'ts
    │   └── best-practices.md  ← Technical standards
    ├── vocabulary.md          ← Semantic dictionary: shorthand, synonyms, project-specific terms
    ├── projects/
    │   └── [project-slug].md  ← One file per project (multi-session missions)
    ├── memory/
    │   ├── active.md          ← Short-term: current work, open issues, where we left off
    │   └── lessons.md         ← Long-term: patterns learned, "never again" items
    └── archive/               ← Aged-out memories
```

**Path resolution:** All references to `data/` in triggers and protocols mean `CORTEX_ROOT/data/`. The agent resolves CORTEX_ROOT once at boot by finding the directory containing this file (cortex.md), then uses relative paths from there.

## Behavioral Rules

1. **Principles are append-only.** Never rewrite or reorganize principles without explicit user approval.
2. **Diary entries are written during sessions**, not reconstructed after. Capture as work happens.
3. **Memory is living.** `active.md` gets updated each session. `lessons.md` is append-only.
4. **Trigger responses are concise.** No lectures. Action, not explanation.
5. **Internal triggers run silently.** The user doesn't see them unless they ask.
6. **The DNA files (cortex.md, README.md) are never modified by genesis.** Genesis only creates the data layer.
7. **Monitoring is boot state.** After `::boot`, the agent is in monitoring mode. All conversation is a knowledge source. When a principle, pattern, lesson, or constraint emerges, capture it to the data layer and briefly note it. When shorthand, synonyms, or project-specific vocabulary emerges, capture it to `data/vocabulary.md`. This isn't a separate activity — it's what "on" means.
8. **Preserve the bootstrap.** When rewriting the agent context file (e.g., `replit.md`) for any reason, the Cortex section MUST be preserved. Check for it after any edit to that file. If it was lost, restore it from the Bootstrap Restoration section below.
9. **Synthesis refines conclusions, not raw material.** When capturing knowledge, connect the user's observations to proper terminology, named patterns, and actionable protocols. Turn "things break at the boundary" into "seam failure prevention" with a structured response. But: raw artifacts (transcripts, diary narratives, source data) stay in their natural form — don't abstract or rewrite them. The readability test: if the user can't recognize their own insight in the synthesized output, it went too far. The goal is "said better," not "said in academese."

## Triggers

Triggers are commands the user types to invoke system behavior. Format: `::code` for no-payload triggers, `::code payload text` for triggers with content. An optional closing `::` delimiter can be used on payload triggers (e.g., `::code payload text::`) but is not required — the agent should parse best-effort and ask if ambiguous. Any trigger with `?` appended shows brief usage help.

### User Triggers

#### ::boot
**Purpose:** Load the system. Orient to current state. Activate passive monitoring.
**Prompt to self:** Read this file (cortex.md). Read data/memory/active.md. Read data/vocabulary.md (the semantic dictionary). Scan data/projects/ for any files with `Status: active` — these are open multi-session missions. Enter **monitoring mode** — from this point forward, continuously watch all conversation for extractable knowledge (principles, patterns, lessons, constraints, vocabulary). When something emerges, capture it to the appropriate data layer file and briefly note it to the user. This is not optional — monitoring is the default state of a booted Cortex. Respond with exactly this format:

```
Cortex online — [project name]
Last diary: [date of most recent diary entry, or "none"]
[one-line summary of active state from active.md]
[if active projects exist: "Active projects: [count] — [names]. Want to continue?"]
Monitoring: active

Type ::? for trigger list.
```

#### ::?
**Purpose:** List all available triggers.
**Prompt to self:** List every user trigger from this file in a compact table: trigger, purpose. No descriptions longer than 8 words.

#### ::ss
**Purpose:** Session start. Full briefing. Load principles into RAM.
**Prompt to self:** Execute ::boot. Read all principles files in full (data/principles/goals.md, constraints.md, best-practices.md) — these are RAM, always loaded. Read data/vocabulary.md (the semantic dictionary). Read the most recent diary entry only (not the full history — diary is disk, searched on demand). Read data/memory/active.md and data/memory/lessons.md (last 10 items). Check data/projects/ for active projects — for each active project, read the file and surface the next incomplete tasks. Report to user: last diary summary (3-4 lines), active memory items, principle count, active projects with next tasks. If active projects exist, nudge: "Hey, we still have [project name] open — [N tasks remaining]. Want to pick that up?" End with "Ready."

#### ::se
**Purpose:** Session end. Write the story, set up the next session.
**Prompt to self:** This trigger has two jobs — write today's permanent record and prepare for tomorrow.
1. **Diary (permanent record):** Review the full conversation. Write/update today's diary narrative (data/diary/YYYY/MM/DD.md) — what happened, what was decided, what was discovered. This is the story. It stays forever. Don't compress or summarize prior entries.
2. **Active memory (working set):** Update data/memory/active.md with: where we left off, open issues, next steps. Flag items older than 5 sessions for archiving.
3. **Principle check:** Monitoring should have captured most principles during the session. Do a final scan — if anything was missed, capture it now.
Respond with: summary of what was written to diary, active memory updates, any new principles captured.

#### ::n payload
**Purpose:** Capture a note to today's diary.
**Prompt to self:** Append the payload text to today's diary file (data/diary/YYYY/MM/DD.md) under a "## Notes" section with timestamp. Create the file and parent directories if they don't exist. Respond: "Noted."

#### ::d
**Purpose:** Write today's diary narrative.
**Prompt to self:** Read today's notes from data/diary/YYYY/MM/DD.md. Review the conversation for additional context. Write an executive summary narrative at the top of the file under "## Summary". Style: release-note tone, include what was accomplished, what went wrong, what was discovered. Keep it under 500 words. Respond: "Diary written." followed by a 2-line preview.

#### ::p payload
**Purpose:** Add a principle.
**Prompt to self:** Parse the payload. Determine which file it belongs in (goals.md, constraints.md, or best-practices.md) based on content. Append it with today's date. Respond: "Added to [file]: [one-line summary]."

#### ::r
**Purpose:** Review all principles before major work.
**Prompt to self:** Read all three principles files in full. Read data/memory/lessons.md. Internalize. Respond: "[count] goals, [count] constraints, [count] best practices, [count] lessons loaded."

#### ::m
**Purpose:** Show active memory.
**Prompt to self:** Read and display data/memory/active.md contents verbatim.

#### ::nt type code description
**Purpose:** Create a new trigger.
**Prompt to self:** Parse: first word = type (diary, principle, memory, protocol, internal, diagnostic), second word = trigger code, remainder = description. Write a new trigger entry in this file (cortex.md) under the appropriate section. Write a concise self-prompt for the trigger based on the description. Respond: "Trigger ::[code] created ([type])."

#### ::nt?
**Purpose:** Show how to create a trigger.
**Prompt to self:** Respond with exactly:
```
::nt type code description
Types: diary, principle, memory, protocol, internal, diagnostic
```

#### ::genesis
**Purpose:** Birth Cortex in a new project. Includes platform detection, a 3-question onboarding interview, project scan, and self-test.
**Guard:** This trigger only works if the agent has already read this file (cortex.md) in the current session. If the user types `::genesis` and the agent doesn't recognize it, respond: "I need to load the Cortex DNA first. Point me to your cortex.md file."
**Prompt to self:** Follow the Genesis Protocol section for the full step-by-step (5 phases: Confirm & Create, Interview, Consent-to-Scan, Self-Test, First Diary Entry). Do NOT copy any existing data — this is a fresh birth. Do NOT modify cortex.md or README.md. Every question asked must write to a file or configure a behavior — no conversation filler.

#### ::ingest
**Purpose:** Absorb recent context into permanent knowledge. A confirmation gesture — "that counts."
**Prompt to self:** Look back at the recent conversation for what the user is referring to — this could be a file they uploaded, a document they mentioned, a discussion that just happened, or a decision that was made. Read/review that material. Extract any knowledge that qualifies as a goal, constraint, best-practice, lesson, or pattern. Append extracted items to the appropriate data layer files (principles/, memory/lessons.md). Respond with a 1-2 sentence synopsis: what was absorbed and where it went. If nothing extractable was found, say so.

**Usage patterns:**
- After uploading a file: "Here's our architecture doc" → `::ingest` → agent reads it, extracts principles
- After a design discussion: user and agent work through a decision → `::ingest` → agent captures the decision as a principle or lesson
- After sharing external research: "I found this article on entity resolution" → `::ingest` → agent extracts relevant patterns
- No path or argument needed — the agent infers what "that" means from conversation context
- If ambiguous, the agent asks: "What should I ingest — the file you uploaded, or the discussion we just had?"

**When you don't need `::ingest`:** Passive monitoring (activated at boot) already captures principles and lessons as they emerge in conversation. Use `::ingest` when you want to deliberately absorb something the monitoring might not catch — like an uploaded file, a long design discussion, or external material you brought in.

#### ::verbatim [N]
**Purpose:** Raw output. Copy the most recent exchange(s) exactly as they happened. No synthesis, no summary, no cleanup.
**Prompt to self:** Copy the most recent user message and agent response EXACTLY as written. If a number N is provided (e.g., `::verbatim 3`), copy the last N exchanges. Default is 1.

**Format — use this exactly:**
```
[User]: (exact user message, copied character for character)

[Agent]: (exact agent response, copied character for character)
```

**What "verbatim" means — follow these rules without exception:**
- Copy the text exactly. Do not paraphrase. Do not rephrase. Do not "clean up."
- Preserve typos, incomplete sentences, informal language, and grammatical errors.
- Preserve line breaks, formatting, and structure as they appeared.
- Do not add introductions, commentary, or transitions between exchanges.
- Do not summarize multiple messages into one. Each message is its own block.
- If in doubt, copy more, not less.

**What a BAD response looks like** (do NOT do this):
```
[User]: The user asked about how transcript features could work in Cortex.
[Agent]: I explained several approaches including bracket triggers and topic-bounded selection.
```

**What a GOOD response looks like** (do this):
```
[User]: could it be something like a default behavior of just literally transcribing the most recent question/answer exchange? sometimes i just need the ability to copy/paste if I want to

[Agent]: Oh — that's much simpler and more practical than what I was overcomplicating. You just want the last exchange, raw, so you can grab it...
```

#### ::wtf payload
**Purpose:** Diagnostic. Something went wrong or user has a question about system behavior.
**Prompt to self:** Parse the payload as a complaint or question. Check the relevant subsystem: did the trigger run? Is the file present? Is the data stale? Diagnose the issue. If fixable, fix it and explain what happened. If not fixable, explain why and suggest a workaround. Keep response under 5 lines.

#### ::proj [payload]
**Purpose:** Create, list, or manage multi-session projects. The agent is the project shepherd — it tracks missions across sessions and nudges when work remains.
**Prompt to self:** Parse the payload to determine the action:

- **No payload** (`::proj`): List all projects in data/projects/. Show name, status, and task progress (e.g., "3/8 complete") for each. Group by status (active first, then completed).
- **`done` or `done [project-name]`** (`::proj done`): Mark the current or specified project as `Status: completed` with today's date. The file stays in data/projects/ — never deleted.
- **Anything else** (`::proj Read and ingest all PRD files`): This is a new project description. Create a new project file:
  1. Generate a slug from the description (e.g., "ingest-prd-files")
  2. Create `data/projects/[slug].md` using the Project File Template below
  3. Break the description into concrete tasks — investigate what's needed (e.g., find the files, estimate scope). If the project involves processing multiple items, list each as a separate task.
  4. If the work will span multiple sessions, note that in the project file.
  5. Respond: "Project created: [name] — [N] tasks. [brief summary of the plan]."

**Shepherd behavior:** At `::boot` and `::ss`, the agent scans data/projects/ for active projects and nudges the user about unfinished work. This is not optional — the agent is the keeper of multi-session continuity.

**Task updates during work:** When working on project tasks during a session, update the project file in real time — check off completed tasks and add session log entries. Don't wait for `::se`.

**Project File Template:**
```
# [Project Name]
Status: active
Created: [YYYY-MM-DD]
Completed: [YYYY-MM-DD or blank]

## Description
[What this project is about and why]

## Tasks
- [ ] [Task 1]
- [ ] [Task 2]
- [ ] [Task 3]

## Session Log
- [YYYY-MM-DD]: [What happened in this session]
```

### ? Help Variant (applies to all triggers)

Any trigger code followed by `?` shows brief usage help for that trigger. Example: `::d?` shows how the diary trigger works. Respond with 1-3 lines max: what it does and what arguments it takes (if any).

### Internal Triggers (agent-initiated, silent)

These fire automatically as part of my workflow. The user doesn't see them unless they ask.

#### after-task-complete
**When:** After completing any task.
**Action:** Scan the work just done for candidate principles. If found, flag to user: "Candidate principle: [summary]. Add with ::p?"

#### after-bug-fix
**When:** After fixing a bug or resolving an error.
**Action:** Capture the failure pattern in data/memory/lessons.md. Format: date, what broke, why, prevention.

#### pre-prd
**When:** Before writing or modifying a PRD.
**Action:** Execute ::r silently. Additionally, check for interface contract registry requirements — ensure the PRD includes boundary definitions for all caller-callee pairs.

#### pre-build
**When:** Before starting implementation of a new feature or major refactor.
**Action:** Execute ::r silently. Check data/memory/active.md for related open issues.

#### vocabulary-capture
**When:** During conversation, when the user uses shorthand, defines a term, establishes a synonym, or coins project-specific vocabulary.
**Action:** Append the term and its meaning to `data/vocabulary.md` in the appropriate section (Cortex Terms, Project Terms, or Shorthand). Briefly note to user: "Added to vocabulary: [term]."

#### memory-maintenance
**When:** At ::se (session end).
**Action:** Review data/memory/active.md. Flag items older than 5 sessions for archiving. Move archived items to data/archive/ with date prefix. Consolidate similar lessons in lessons.md if count exceeds 30.

#### assess
**When:** Periodically during sessions — before and after major work blocks, and whenever the agent suspects it may have drifted from protocol.
**Action:** Silent self-diagnostic. Check:
1. **Principles loaded?** Were goals.md, constraints.md, best-practices.md actually read this session, or is the agent operating on assumptions?
2. **Bootstrap intact?** Quick verify that the Cortex section in replit.md hasn't been clobbered by a rewrite.
3. **Monitoring active?** Has the agent been capturing principles/vocabulary/lessons during conversation, or has it gone heads-down and stopped noticing?
4. **Project continuity?** Is the active project file being updated in real-time as tasks complete, or has the agent forgotten?
5. **Memory hygiene?** Is the agent working from active.md or from stale assumptions carried over from earlier in the conversation?
No output to the user unless something is wrong. If a check fails, the agent fixes it silently or flags it briefly: "Assess: [what's off]. Fixing."

## Memory Architecture

Cortex has two tiers of permanent memory with different access patterns:

### Principles = RAM (always loaded)

Files: `data/principles/goals.md`, `constraints.md`, `best-practices.md`

Always in context. Loaded at every `::boot` and `::ss`. These are the operating rules — dense, distilled, actionable. Every decision gets checked against them. Passive monitoring writes to these in real time as knowledge emerges. Principles are **permanent and append-only** — they never age out, never get archived, never get compressed.

### Diary = Disk (permanent record, searched on demand)

Files: `data/diary/YYYY/MM/DD.md`

The story of what happened. Rich, detailed, one entry per day. Written during sessions (rule #2) and finalized at `::se`. Diary entries are **permanent** — never deleted, never summarized-and-replaced. They accumulate forever. But they are **not bulk-loaded into context** — only the most recent entry is read at `::ss` for orientation. Older entries are searched on demand when the user or agent needs the history ("what happened when we built X?").

### Active Memory = Working Set

Files: `data/memory/active.md`, `data/memory/lessons.md`

Current state: where we left off, open issues, next steps. This is the only tier that ages. Items in `active.md` become stale as work moves on. `lessons.md` is append-only but its items can age from hot to archived.

### Projects = Multi-Session Missions

Files: `data/projects/[slug].md`

Missions that span multiple sessions. Each project has a description, a task list, and a session log. Projects are **permanent** — completed projects are marked done but never deleted. Active projects are surfaced at every `::boot` and `::ss` so the agent can shepherd them to completion. Created via `::proj`, managed in real time during sessions.

### Why This Matters

The distinction prevents two failure modes:
1. **Context pollution** — loading 30 days of diary into every session drowns the useful signal (principles) in narrative noise.
2. **Knowledge loss** — compressing or deleting diary entries destroys the historical record. Sometimes you need the story, not just the lesson.

## Memory Aging Protocol

Aging applies to `data/memory/` items only. Principles and diary entries are permanent and do not age.

Active memory items (`active.md`) have implicit timestamps from when they were created/last referenced.

- **Hot:** Referenced in the last 3 sessions. Always surfaced at `::ss`.
- **Warm:** Referenced in the last 5-10 sessions. Surfaced only on `::r` or `::m`.
- **Cold:** Not referenced in 10+ sessions. Candidate for archiving. At `::se`, suggest archiving.
- **Archived:** Moved to `data/archive/`. Not surfaced unless explicitly searched. Never deleted.

## Portability

Cortex is designed to reproduce. The DNA is two files: **cortex.md** (this file) and **README.md**. Drop them anywhere in a project, tell the agent to read cortex.md, run genesis, and a new Cortex is born — complete with the ability to reproduce into yet another project.

### How to Port

1. Copy two files into the new project — anywhere you like:
   - `cortex.md` (this file — the operating manual)
   - `README.md` (the quick-start)
2. Tell the agent: **"Read and act on `[path-to]/cortex.md`"** — This loads the DNA. The agent now understands the trigger system. The verb "act on" is critical — "read and follow" causes agents to acknowledge the file without executing its instructions.
3. Type `::genesis` — the agent auto-detects where cortex.md lives (CORTEX_ROOT), creates the data layer as a sibling directory, interviews the user, generates vision.md, scans the project, self-tests, and writes the birth diary.

That's it. No prescribed directory structure. No files to pre-create. The new Cortex is fully functional and can itself be ported to yet another project.

**Why step 2 matters:** Triggers like `::genesis` are meaningless to an agent that hasn't loaded cortex.md. The agent must read the DNA first before any triggers work. Using "act on" instead of "follow" is the difference between the agent executing the instructions and merely noting that instructions exist.

### Platform Adaptation

The only platform-specific piece is the bootstrap hook — the file where the agent looks for project context on startup. Genesis writes the bootstrap to this file automatically.

| Platform | Bootstrap file | Notes |
|----------|---------------|-------|
| Replit | `replit.md` | Read automatically by Replit agents |
| Claude Code | `CLAUDE.md` | Read automatically by Claude |
| Cursor | `.cursorrules` | Read automatically by Cursor |
| Windsurf | `.windsurfrules` | Read automatically by Windsurf |
| Other | Project README or equivalent | Wherever the agent looks for context |

The bootstrap template content stays the same across platforms — only the target file and the path to cortex.md change. The path in the bootstrap must point to wherever cortex.md actually lives in the project.

## Genesis Protocol

Genesis has five phases. Each phase completes before the next begins. Every question asked must produce something the system uses — no conversation for conversation's sake.

**Prerequisites:**
- cortex.md and README.md must exist somewhere in the project. Genesis auto-detects where they are.
- The agent must have already read this file (cortex.md) in the current session. If the agent doesn't recognize `::genesis`, the user needs to point the agent to cortex.md first.
- See **Portability > How to Port** for the full setup sequence.

### Phase 1: Confirm & Create

1. Verify this is intentional (respond: "Birth Cortex here? This creates the data layer and configures the system. Type 'yes' to confirm.")
2. **Resolve CORTEX_ROOT** — the directory containing this file (cortex.md). All paths below are relative to CORTEX_ROOT. Report: "CORTEX_ROOT: [resolved path]"
3. Detect platform automatically (check for replit.md, CLAUDE.md, .cursorrules, .windsurfrules). Report which platform was detected.
4. Create: data/diary/, data/principles/, data/memory/, data/projects/, data/archive/
5. Create empty seed files: data/principles/goals.md, data/principles/constraints.md, data/principles/best-practices.md, data/memory/active.md, data/memory/lessons.md, data/vocabulary.md
6. Create data/what-is-cortex.md from template (section below)
7. Create data/birth-story.md
8. Add Cortex bootstrap to the detected platform's agent context file — use the exact template from the **Bootstrap Restoration** section below. The path in the bootstrap must point to CORTEX_ROOT/cortex.md.
9. Do NOT modify cortex.md or README.md — those are the DNA, already present.

### Phase 2: Interview (3 questions)

Ask these three questions. Each one writes directly to the data layer.

1. **"What's this project about, in a sentence?"** → Seeds `data/principles/goals.md` with the project's purpose. Also generates `data/vision.md` — a full elevator-pitch document synthesized from the answer, explaining what the project is, the problem it solves, and why it matters. Use the Vision Template below.
2. **"Should I be concise or detailed when I talk to you?"** → Seeds `data/principles/constraints.md` with communication style preference.
3. **"Should I actively capture principles and patterns as we work, or wait for you to flag them?"** → Configures monitoring aggressiveness in `data/principles/constraints.md`. If active: monitoring is always on (default Cortex behavior). If passive: monitoring only captures when the user uses `::p` or `::ingest`.

### Phase 3: Consent-to-Scan

Ask: **"I'd like to look around the project now — scan the file structure, check for documentation, see what frameworks you're using, look at git history. OK to proceed?"**

If yes, perform the scan and report results conversationally as they're found:
1. **File structure** — language, framework, key directories. Report: "Found a [language]/[framework] project..."
2. **Documentation** — scan for docs/, PRDs, READMEs, design files. Report: "Found [N] documents in [location]..."
3. **Git history** — author count, age, commit frequency. Report: "Git shows [details]..."
4. **Dependencies** — package manager, key libraries. Report: "Using [key dependencies]..."
5. **Existing conventions** — code style, patterns, architecture. Report: "Noticed [patterns]..."

Write findings to `data/memory/active.md` under a "## Project Scan" section.

After the scan, ask **1-2 follow-up questions** that are specific to what was discovered — questions that couldn't have been asked before the scan. Examples:
- "I see 12 PRDs in docs/. Should I absorb those into memory, or are some outdated?"
- "There's a test infrastructure but no CI config. Is automated testing a priority?"
- "The codebase has two competing patterns for [X]. Which do you prefer?"

Only ask follow-ups if the scan surfaced something genuinely ambiguous. If everything is clear, skip to Phase 4.

### Phase 4: Self-Test

Run a verification sequence and report results:

1. **File I/O** — Write a test note to today's diary (`::n Genesis self-test`), read it back, confirm it persists. Report: pass/fail.
2. **Principle capture** — The project description from Phase 2 should already be in goals.md. Read it back and confirm. Report: pass/fail.
3. **Boot sequence** — Execute `::boot` and confirm it produces the expected output format (project name, last diary date, active state summary, monitoring status). Report: pass/fail.
4. **Bootstrap check** — Read the platform context file and confirm the Cortex bootstrap section is present and uses the correct directive language. Report: pass/fail.

If any test fails, fix it immediately and re-test. Report: "All systems verified" or "Fixed [issue], all systems verified."

### Phase 5: First Diary Entry

Write the birth diary entry at `data/diary/YYYY/MM/DD.md` containing:
- CORTEX_ROOT location
- What was created (data layer, bootstrap, vision.md)
- Platform detected
- Interview answers and how they configured the system
- Scan findings (if consent was given)
- Self-test results

Respond: "Cortex born and verified. Type `::?` for trigger list, or just start working — I'm monitoring."

## What-Is-Cortex Template

Used by genesis to create what-is-cortex.md in new projects:

```
# What is Cortex?

Cortex is a collaborative memory system between a human and an AI agent.

It solves three problems:
1. AI agents lose all context between sessions. Cortex gives them persistent memory.
2. Projects accumulate hard-won knowledge (principles, patterns, lessons) that gets lost. Cortex captures and organizes it.
3. There's no protocol for when and how an agent should refresh its memory. Cortex defines explicit triggers.

## How It Works

The system has two layers:
- **DNA** (cortex.md + README.md) — The portable core. Contains all trigger definitions, prompts, protocols, and behavioral rules. Carry these two files to any project.
- **Data layer** (data/) — The memories. Diary entries, principles, vision, active memory, lessons learned. Generated by genesis, unique to each project.

## Triggers

Type ::? to see all available triggers. Type ::boot to start.

## Design Philosophy

- Human-readable files, not opaque embeddings
- Collaborative — both human and agent contribute
- Explicit protocols over implicit hope
- Append-only principles, living memory
- The system reproduces itself via ::genesis
```

## Vision Template

Used by genesis Phase 2 to generate data/vision.md from the user's project description. The agent synthesizes this from the one-sentence project answer, expanding it into a full pitch:

```
# [Project Name]: Why It Exists

## The Problem
[What problem does this project solve? Why does the current state of things fall short?]

## What [Project Name] Is
[One-paragraph description of what the project does and how it works at a high level.]

## What It Provides
[Key capabilities — 3-5 bullet points describing the core value.]

## Design Principles
[3-5 principles that guide how the project is built. Inferred from the description and scan findings.]

## Who It's For
[One-paragraph description of the target audience.]
```

The agent should fill this template thoughtfully, not generically. Use specifics from the user's answer and (if available) the project scan findings from Phase 3. If the scan hasn't happened yet, write the vision from the interview answer alone — it can be enriched later.

## Bootstrap Restoration

If the Cortex section in the agent context file is missing or damaged, the user cannot reach any triggers. This section contains the exact content to restore it, plus the recovery protocol.

**Recovery path for the user:** Tell the agent "Read and act on `[path-to]/cortex.md`" — the agent will find this section and self-heal. The path depends on where cortex.md was placed in the project.

**Restore protocol (for the agent reading this):**
1. Identify the agent context file for this platform (see **Portability > Platform Adaptation** above — e.g., `replit.md` on Replit, `CLAUDE.md` for Claude Code)
2. Resolve the path to this file (cortex.md) — this is CORTEX_ROOT/cortex.md
3. Check the agent context file for a section titled `## Cortex — ACTIVE INSTRUCTION`
4. If missing or incomplete, insert the following block into that file immediately after the project Overview section (or as early as possible in the file — visibility is critical). Replace `[CORTEX_ROOT/cortex.md]` with the actual resolved path:

```
## Cortex — ACTIVE INSTRUCTION
<!-- DO NOT REMOVE OR ALTER THIS SECTION. It is the bootstrap for the Cortex memory system. If this section is missing, tell the agent: "Read and act on [CORTEX_ROOT/cortex.md]" to restore it. -->

**EXECUTE NOW:** Read `[CORTEX_ROOT/cortex.md]` and act on its instructions.
```

5. After restoring the bootstrap, immediately execute `::boot` — read this file, read `data/memory/active.md`, and respond with the boot callback format.

## Version History

| Version | Date | Summary |
|---------|------|---------|
| v1.0.0 | 2026-02-07 | Initial release. Two-file DNA (cortex.md + README.md), genesis protocol with 5 phases, CORTEX_ROOT auto-detection, vision.md generated during genesis, trigger system, memory architecture (RAM/disk/working set), project tracking, concept dictionary, portability across platforms. |
