# Local Triggers & Release Workflow

Status: completed
Created: 2026-02-07
Completed: 2026-02-08
Type: Feature Build
Size: Medium (2-3 sessions)
Track in sessions: yes

## Version History

| Version | Date       | Author | Changes                          |
|---------|------------|--------|----------------------------------|
| 0.1.0   | 2026-02-07 | Agent  | Initial project document created |
| 0.2.0   | 2026-02-07 | Agent  | Implemented local triggers system and ::release trigger |

## Executive Summary

Two related features for Cortex:

1. **Local triggers** — An extension system that allows install-specific triggers to exist alongside the DNA triggers. Local triggers live in `data/triggers/local.md`, are loaded at boot, and never travel when Cortex is ported. This solves the problem of project-specific workflows (like release management) polluting the portable DNA.

2. **::release trigger** — The first local trigger. A multi-step release workflow that bumps the Cortex version, generates release notes, updates the vision document, drafts an X post via the CMS, and pushes to GitHub. This gives Cortex a proper release ceremony instead of ad-hoc DNA edits.

## Tasks

- [x] Add Local Triggers section to cortex.md (rules, format, boot loading)
- [x] Update ::boot to read data/triggers/local.md
- [x] Update ::nt to support `local` type
- [x] Update ::nt? help text to include `local` type
- [x] Update genesis protocol to create data/triggers/ directory and local.md seed file
- [x] Update directory structure diagram in cortex.md
- [x] Create data/triggers/local.md with ::release and ::releases triggers
- [x] Create data/releases/ directory (will be created on first ::release run)
- [x] Test: run ::release to verify the full workflow

## Success Criteria

- Local triggers load at boot without errors
- `::?` lists local triggers with [local] tag
- `::nt local` creates triggers in local.md, not cortex.md
- `::release` produces version bump, release notes, vision check, X post draft, and GitHub push
- Local triggers do NOT appear in cortex.md DNA
- Porting Cortex to a new project does NOT carry local triggers

## Notes

- The ::release trigger interacts with the X CMS API (POST /api/posts) to draft announcements. This only works in this Replit project where the CMS is running.
- data/releases/ directory is created on demand by ::release, not by genesis. This keeps genesis clean — most installs won't need a releases directory.

## Session Log

- 2026-02-07: Project created. Implemented local triggers system in cortex.md (section, boot loading, ::nt update, genesis update, directory structure). Created data/triggers/local.md with ::release and ::releases triggers. Architect review caught: ::ss not explicitly loading local triggers (fixed — ::ss executes ::boot which loads them), ::? not updated to list local triggers with [local] tag (fixed), conflict detection at boot not specified (fixed with explicit check-and-warn behavior), ::release CMS payload and GitHub check not explicit enough (fixed with POST body spec and git remote check).
- 2026-02-08: Created data/releases/ directory. Built Releases page in DNA Editor (Phase 3) — parseReleases() parser, GET /api/cortex/releases endpoint, cortex-releases.tsx page with expandable cards and change categories. 8/9 tasks complete. Remaining: test ::release workflow end-to-end.
- 2026-02-08: Ran ::release v1.1.0 end-to-end. Version bumped in cortex.md, release notes generated at data/releases/v1.1.0.md, vision unchanged, X post drafted, GitHub push. All 9/9 tasks complete.
- 2026-02-08: Post-release fix — created GitHub Release object (v1.1.0) via Releases API. Repo "About" was still showing v1.0.0 because commit alone doesn't create a Release. Updated ::release best practice to include this step.
