# Active Memory

## Project Scan (2026-02-07)
- **Stack:** TypeScript fullstack — React + Vite (client), Express (server)
- **UI:** Shadcn components, Tailwind CSS, Radix UI primitives
- **Data:** Drizzle ORM + PostgreSQL, TanStack Query for fetching
- **Routing:** Wouter
- **Cortex DNA:** Pulled from GitHub (dvn66/cortex), placed in cortex/

## Current State (2026-02-08)
- X content management system is live and functional
- Features: single post and thread composition, scheduling, status workflow (draft/scheduled/posted), copy-to-clipboard
- Dashboard with stats cards and tabbed post lists
- Dark mode support
- **DNA Editor fully shipped** — all 7 pages live (Overview, Triggers, Principles, Memory, Projects, Templates, Releases)
- All 7 DNA Editor pages have full CRUD where applicable
- 14 Cortex API endpoints with Zod validation
- Parser: cortex-parser.ts handles all cortex data extraction
- Writer: cortex-writer.ts handles all writes with atomic ops, .bak backups, path traversal prevention
- Sidebar split into two groups: X CMS + Cortex DNA (7 items)
- **Cortex v1.1.0 released** — pushed to GitHub (dvn66/cortex), GitHub Release created

## Where We Left Off
- v1.1.0 release cycle complete (commit + GitHub Release)
- GitHub push best practice hardened: must create both commit and Release object
- User asked about X account profile storage — no decision made yet (DNA vs database)
- Phase 4 scope: Polish, cross-page search, bulk operations

## Active Projects
- **Cortex Cross-Platform Portability Testing** — active, 0/9 tasks complete, not started yet

## Completed Projects
- **Local Triggers & Release Workflow** — completed 2026-02-08, 9/9 tasks
- **::proj Trigger Upgrade** — completed 2026-02-07, 10/10 tasks

## Open Items
- No X API integration (manual posting workflow by design)
- X account profile info storage location undecided
- best-practices.md has 4 entries
- lessons.md has 2 entries (CoVe technique, auto-session-end gap)
- vocabulary.md has empty sections — no terms captured yet

## Lessons Learned
- Drizzle date handling: when receiving ISO strings from frontend JSON, must explicitly convert to Date objects before passing to Drizzle
- Thread model: parent post has type="thread" with threadId=null, child posts reference parent via threadId with threadOrder for sequencing
- Architect tool has a file size limit in diff view — large files get truncated, causing false negative reviews
- Markdown parser for triggers: H4 headers define block boundaries, Purpose/Prompt-to-self are the two required fields per block
- Badge styling: always use design system variants instead of custom bg colors
- Error states are essential on every data-fetching page
- Parser architecture: extractSection() helper is reusable across different file types
- GitHub commits and GitHub Releases are separate objects — pushing a commit alone doesn't create a release
