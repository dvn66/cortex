# Cortex Cross-Platform Portability Testing

Status: active
Created: 2026-02-07
Completed:

## Version History

| Version | Date       | Author | Changes                              |
|---------|------------|--------|--------------------------------------|
| 0.1.0   | 2026-02-07 | Agent  | Initial project document created     |

## Executive Summary

Cortex claims to be portable — drop two DNA files (cortex.md, README.md) into any project, tell the agent to read them, run genesis, and a fully functional memory system is born. This project validates that claim across five agentic IDE platforms.

**Why this matters:** If Cortex only works on Replit, it's a Replit feature. If it works everywhere, it's a system. Portability is the difference between a tool and a protocol.

**Scope:** Test the full Cortex lifecycle (genesis → boot → session workflow → session continuity) on each target platform. Document what works, what breaks, and what platform-specific adaptations are needed.

**Success threshold:** Cortex is considered portable if it passes all critical tests on 4 of 5 platforms (80%). Platform-specific quirks are acceptable if they can be resolved with documented workarounds — not DNA rewrites.

---

## Platforms Under Test

| # | Platform       | Bootstrap File   | Agent Type         | Status      |
|---|----------------|------------------|--------------------|-------------|
| 1 | Replit         | `replit.md`      | Replit Agent       | Baseline    |
| 2 | Cursor         | `.cursorrules`   | Cursor Agent       | Not started |
| 3 | Windsurf       | `.windsurfrules` | Codeium Agent      | Not started |
| 4 | Claude Code    | `CLAUDE.md`      | Anthropic CLI      | Not started |
| 5 | Bolt (StackBlitz) | TBD           | Bolt Agent         | Not started |

---

## Success Metrics

Each platform is evaluated against six test categories. Each test is scored **Pass**, **Partial** (works with workaround), or **Fail**.

### Test Categories

| #  | Test                    | What it validates                                                     | Pass criteria                                                                 |
|----|-------------------------|-----------------------------------------------------------------------|-------------------------------------------------------------------------------|
| T1 | **Genesis**             | Data layer creation, platform detection, interview, self-test         | All Phase 1–5 steps complete. data/ directory structure matches spec.         |
| T2 | **Boot (::boot)**       | System loads, reads active memory, enters monitoring mode             | Correct boot output format. Monitoring active.                                |
| T3 | **Trigger System**      | Core triggers fire correctly (::ss, ::se, ::d, ::n, ::p, ::r, ::m)   | At least 5 of 7 triggers produce correct behavior.                            |
| T4 | **Data Persistence**    | Files written during session are readable in next session             | Diary, principles, and active memory survive session boundary.                |
| T5 | **Session Continuity**  | ::se → close → reopen → ::ss restores context                        | Agent accurately reports last session state. No data loss.                    |
| T6 | **Monitoring Mode**     | Passive capture of principles/vocabulary during conversation          | At least 1 principle or vocabulary item captured without explicit trigger.     |

### Scoring

| Score   | Meaning                                                    |
|---------|------------------------------------------------------------|
| **Pass**    | Works as specified, no modifications needed            |
| **Partial** | Works with documented workaround or minor adaptation   |
| **Fail**    | Does not work, no reasonable workaround found          |
| **N/A**     | Platform cannot support this test (documented why)     |

### Overall Platform Verdict

| Verdict        | Criteria                                      |
|----------------|-----------------------------------------------|
| **Compatible** | T1–T5 all Pass or Partial. T6 Pass or Partial.|
| **Usable**     | T1–T4 Pass or Partial. T5 or T6 may Fail.     |
| **Incompatible** | T1 or T2 Fail.                              |

---

## Tasks

- [ ] Define test protocol script (exact steps a tester follows per platform)
- [ ] Test on Replit (baseline — confirm all T1–T6 pass)
- [ ] Test on Cursor
- [ ] Test on Windsurf
- [ ] Test on Claude Code
- [ ] Test on Bolt (StackBlitz)
- [ ] Compile results matrix
- [ ] Write summary report with platform-specific findings
- [ ] Update cortex.md with any portability fixes discovered

---

## Test Protocol (per platform)

> Follow these exact steps on each platform. Record results in the platform's section below.

1. **Setup** — Create a new project on the platform. Copy `cortex.md` and `README.md` into a `cortex/` directory (or project root).
2. **Load DNA** — Tell the agent: "Read and act on cortex/cortex.md"
3. **Genesis** — Type `::genesis`. Walk through all 5 phases. Record any errors or deviations.
4. **Verify data layer** — Check that `data/` directory was created with the expected structure.
5. **Boot** — Type `::boot`. Verify output matches the specified format.
6. **Trigger sweep** — Run each trigger and verify behavior:
   - `::n Test note from portability testing` → check diary file
   - `::d` → check diary summary written
   - `::p Always validate inputs at API boundaries` → check principles file
   - `::r` → verify principle count output
   - `::m` → verify active memory displayed
   - `::ss` → verify full session start briefing
   - `::se` → verify session end (diary, active memory, principle check)
7. **Session continuity** — Close the session/conversation entirely. Start a new one. Boot Cortex. Verify it remembers what happened.
8. **Monitoring test** — Have a natural conversation about a design decision. Check if the agent captures a principle or vocabulary item without being asked.
9. **Record results** — Fill in the platform section below.

---

## Platform Results

### 1. Replit (Baseline)

**Status:** Not started
**Tester:**
**Date:**

| Test | Result | Notes |
|------|--------|-------|
| T1 Genesis        |   |   |
| T2 Boot           |   |   |
| T3 Triggers       |   |   |
| T4 Data Persist   |   |   |
| T5 Session Cont.  |   |   |
| T6 Monitoring     |   |   |

**Verdict:**

**Platform Notes:**
- Baseline platform. Cortex was built here.
- Bootstrap file: `replit.md`
- Known behaviors:

---

### 2. Cursor

**Status:** Not started
**Tester:**
**Date:**

| Test | Result | Notes |
|------|--------|-------|
| T1 Genesis        |   |   |
| T2 Boot           |   |   |
| T3 Triggers       |   |   |
| T4 Data Persist   |   |   |
| T5 Session Cont.  |   |   |
| T6 Monitoring     |   |   |

**Verdict:**

**Platform Notes:**
- Bootstrap file: `.cursorrules`
- Agent model: varies (user-configurable)
- File system: local (native OS)
- Known considerations:

---

### 3. Windsurf

**Status:** Not started
**Tester:**
**Date:**

| Test | Result | Notes |
|------|--------|-------|
| T1 Genesis        |   |   |
| T2 Boot           |   |   |
| T3 Triggers       |   |   |
| T4 Data Persist   |   |   |
| T5 Session Cont.  |   |   |
| T6 Monitoring     |   |   |

**Verdict:**

**Platform Notes:**
- Bootstrap file: `.windsurfrules`
- Agent: Codeium/Windsurf AI
- Known considerations:

---

### 4. Claude Code

**Status:** Not started
**Tester:**
**Date:**

| Test | Result | Notes |
|------|--------|-------|
| T1 Genesis        |   |   |
| T2 Boot           |   |   |
| T3 Triggers       |   |   |
| T4 Data Persist   |   |   |
| T5 Session Cont.  |   |   |
| T6 Monitoring     |   |   |

**Verdict:**

**Platform Notes:**
- Bootstrap file: `CLAUDE.md`
- Agent: Claude (terminal-based, no IDE GUI)
- Interaction model: CLI — may affect trigger parsing
- Known considerations:

---

### 5. Bolt (StackBlitz)

**Status:** Not started
**Tester:**
**Date:**

| Test | Result | Notes |
|------|--------|-------|
| T1 Genesis        |   |   |
| T2 Boot           |   |   |
| T3 Triggers       |   |   |
| T4 Data Persist   |   |   |
| T5 Session Cont.  |   |   |
| T6 Monitoring     |   |   |

**Verdict:**

**Platform Notes:**
- Bootstrap file: TBD (needs investigation)
- Agent: Bolt AI
- Environment: WebContainer (browser-based file system)
- Known considerations: file system is virtual, may affect persistence across sessions

---

## Results Summary

> Populated after all testing is complete.

| Platform       | T1 | T2 | T3 | T4 | T5 | T6 | Verdict |
|----------------|----|----|----|----|----|----|---------|
| Replit         |    |    |    |    |    |    |         |
| Cursor         |    |    |    |    |    |    |         |
| Windsurf       |    |    |    |    |    |    |         |
| Claude Code    |    |    |    |    |    |    |         |
| Bolt           |    |    |    |    |    |    |         |

**Overall portability score:** ___ / 5 platforms compatible

---

## Findings & Adaptations

> Document any changes needed to cortex.md or README.md to improve portability.

| Finding | Platform(s) | Severity | Resolution |
|---------|-------------|----------|------------|
|         |             |          |            |

---

## Session Log

- 2026-02-07: Project created. Defined 5 target platforms, 6 test categories, formal test protocol, and per-platform result tracking.
