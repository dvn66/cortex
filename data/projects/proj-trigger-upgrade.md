# ::proj Trigger Upgrade

Status: completed
Created: 2026-02-07
Completed: 2026-02-07
Type: Feature Build
Size: Medium (2-3 sessions)
Track in sessions: yes

## Version History

| Version | Date       | Author | Changes                                              |
|---------|------------|--------|------------------------------------------------------|
| 0.1.0   | 2026-02-07 | Agent  | Initial project document created                     |
| 0.2.0   | 2026-02-07 | Agent  | Resolved open questions, implemented all DNA changes |

## Executive Summary

Upgrade the `::proj` trigger from a minimal project stub generator into a structured project creation feature. The current trigger takes a one-line description and guesses at tasks. The upgraded version includes:

- **Interview-driven creation** — 3 quick-pick questions (type, size, session tracking) plus 1 optional free-text question
- **Template composition** — 5 project types (Feature Build, Testing, Research, Refactor, Other) assembled from 10 reusable template blocks stored in `data/templates/`
- **Project dashboard** — `::proj` with no payload shows all projects grouped by Active, Dormant, Completed
- **Session integration** — `::ss` and `::se` now include project status (verbose for tracked, quiet for untracked, nudge for dormant)
- **Backward compatible** — quick one-liners still create lightweight projects without the interview

This is a DNA-level change — it modifies `cortex.md` itself and adds template files to the data layer.

## Resolved Decisions

- Templates: agent presents project types as multiple choice during interview
- Interview depth: 3 quick-pick + 1 optional open-ended = under 30 seconds
- Template storage: separate files in `data/templates/` with a README documenting the composition matrix
- Backward compatible: yes — small obvious tasks skip the interview automatically

## Tasks

- [x] Resolve open questions with user
- [x] Define project templates (types, structure, required fields)
- [x] Design the interview flow (questions, what each produces)
- [x] Draft the updated `::proj` trigger spec for cortex.md
- [x] Create template files in data/templates/
- [x] Update cortex.md with new ::proj behavior
- [x] Update ::ss trigger to include tiered project status reporting
- [x] Update ::se trigger to include project updates step
- [x] Test: create a project using new flow, verify output quality
- [x] Update README.md if the ::proj section needs reflecting (reviewed — existing entry is generic enough, no changes needed)

## Success Criteria

- New `::proj` flow produces project documents at least as good as the cross-platform testing doc (cortex-cross-platform-testing.md)
- Interview takes under 30 seconds (all quick-pick, no open-ended required)
- Template selection feels natural, not bureaucratic
- Backward-compatible: a quick `::proj do the thing` still works without forcing the full interview
- `::proj` with no payload shows a useful dashboard of all projects
- `::ss` and `::se` correctly report project status at appropriate verbosity levels

## Notes

- The cross-platform testing project (cortex-cross-platform-testing.md) was created before this upgrade — it predates the template system but serves as the quality benchmark for what generated project docs should look like.
- "Dormant" is a computed status, not stored — any active project with no session log entry in 5+ sessions is considered dormant.

## Session Log

- 2026-02-07: Project created. Open questions surfaced to user for input before implementation begins.
- 2026-02-07: User resolved all open questions. Implemented: updated ::proj trigger spec in cortex.md with interview flow, template composition system, dashboard, and quick-create shortcut. Created 10 template files in data/templates/. Updated ::ss and ::se triggers for tiered project status reporting. Verified README needs no changes. All tasks complete.
