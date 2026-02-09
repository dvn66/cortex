# Active Memory

## Project Identity
- **X handle:** @cortex_mem
- **GitHub repo:** dvn66/cortex
- **GitHub raw URL:** https://raw.githubusercontent.com/dvn66/cortex/main/cortex.md
- **One-liner fetch:** Fetch https://raw.githubusercontent.com/dvn66/cortex/main/cortex.md, save it to this project, read it, and run ::genesis
- **Install prompt (public-facing):** Grab cortex.md from github.com/dvn66/cortex and follow its instructions.

## Project Scan (2026-02-07)
- **Stack:** TypeScript fullstack — React + Vite (client), Express (server)
- **UI:** Shadcn components, Tailwind CSS, Radix UI primitives
- **Data:** Drizzle ORM + PostgreSQL, TanStack Query for fetching
- **Routing:** Wouter
- **Cortex DNA:** Pulled from GitHub (dvn66/cortex), placed in cortex/

## Current State (2026-02-09)
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
- **Cortex v1.5.0 released** — v1.4.0 pushed to GitHub, v1.5.0 push pending (rate limited)
- **Single-file DNA model adopted** — cortex.md is the only portable file. README.md is the GitHub repo landing page, not part of portable DNA.

## Where We Left Off (2026-02-09)
- Released v1.4.0 (boot verification, passphrase "context will survive", lessons.md in boot sequence, project identity in active.md)
- Released v1.5.0 (::update trigger for self-updating DNA from GitHub, boot version check)
- v1.4.0 pushed to GitHub successfully (commit + Release)
- v1.5.0 GitHub push pending — rate limited after v1.4.0 push. Files ready locally, just needs retry.
- Discussed memory drift across sessions — existing boot defenses are solid, no new safeguards needed yet
- README.md updated with ::update trigger in trigger table

## Active Projects
- **Cortex Cross-Platform Portability Testing** — active, 0/9 tasks complete, not started yet
- **Agentic Platform Landscape Research** — active, 5/5 tasks complete, PRD at docs/prd-agentic-platform-landscape.md
- **X Content Strategy & Rollout** — active, 6/9 tasks complete, 13 new posts drafted, ready for posting

## Completed Projects
- **Local Triggers & Release Workflow** — completed 2026-02-08, 9/9 tasks
- **::proj Trigger Upgrade** — completed 2026-02-07, 10/10 tasks

## Open Items
- v1.5.0 GitHub push pending (rate limit should clear soon — retry next session)
- No X API integration (manual posting workflow by design)
- Phase 4 scope: Polish, cross-page search, bulk operations
- Cross-platform portability testing not started (0/9 tasks)
- Portability test project needs update: remove ChatGPT/Bolt, confirm single-file onboarding path
- Compatibility matrix added to README.md (T1-T6 scores for 10 platforms, timestamped)
- ::release trigger updated: step 5 now updates compatibility matrix in README + PRD on each release

## Lessons Learned
- Drizzle date handling: when receiving ISO strings from frontend JSON, must explicitly convert to Date objects before passing to Drizzle
- Thread model: parent post has type="thread" with threadId=null, child posts reference parent via threadId with threadOrder for sequencing
- Architect tool has a file size limit in diff view — large files get truncated, causing false negative reviews
- Markdown parser for triggers: H4 headers define block boundaries, Purpose/Prompt-to-self are the two required fields per block
- Badge styling: always use design system variants instead of custom bg colors
- Error states are essential on every data-fetching page
- Parser architecture: extractSection() helper is reusable across different file types
- GitHub commits and GitHub Releases are separate objects — pushing a commit alone doesn't create a release
- GitHub rate limiting is aggressive on write endpoints — space out pushes or expect 429s that persist for several minutes
