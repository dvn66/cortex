# Agentic Platform Landscape Research

Status: active
Created: 2026-02-09
Completed:
Type: Research
Size: Quick (1 session)
Track in sessions: yes

## Executive Summary

Research project to catalog the agentic coding platform landscape and create a formalized PRD tracking Cortex compatibility across all qualifying platforms. Identifies 10 platforms that meet the criteria: agentic (AI writes code), persistent projects across sessions, and no comprehensive built-in memory system.

The PRD lives at `docs/prd-agentic-platform-landscape.md` and includes per-platform profiles (features, target market, users, revenue), a Cortex compatibility matrix aligned with T1-T6 test categories, and priority tiers for testing.

## Tasks

- [x] Research all agentic coding platforms (Cursor, Windsurf, Claude Code, Bolt, Lovable, v0, VibeCodeApp, Cline, Aider, Replit)
- [x] Compile features, target market, and popularity metrics for each
- [x] Create formalized PRD with executive summary, platform profiles, compatibility matrix
- [x] Save PRD to docs/ folder with versioning and date stamps
- [x] Create project file and update active memory

## Success Criteria

- Comprehensive list of qualifying platforms (minimum 8)
- Each platform has: name, type, features summary, target market, user count/revenue, persistence model, memory system status, Cortex compatibility notes
- Compatibility matrix with T1-T6 scoring aligned with existing portability testing project
- Platform priority tiers based on market size and Cortex fit
- Document is versioned and date-stamped

## Findings

- 10 platforms qualify across 4 categories: Desktop IDEs (Cursor, Windsurf), Terminal CLIs (Claude Code, Aider), Cloud platforms (Replit, Bolt, Lovable, v0), VS Code extensions (Cline), Mobile (VibeCodeApp)
- No platform has solved persistent agent memory comprehensively — Cortex is genuinely differentiated
- Config file conventions (.cursorrules, .windsurfrules, CLAUDE.md, replit.md) are Cortex's bootstrap path on each platform
- Tier 1 priorities: Cursor (1M+ users, $500M ARR), Windsurf (1M+ users, $100M ARR), Claude Code (115K+ devs)
- Claude Code has the most competing memory infrastructure (built-in Memory + claude-mem plugin)
- Cloud platforms (Bolt, Lovable, v0) have uncertain filesystem access — needs investigation

## Notes

- This project complements the existing "Cortex Cross-Platform Portability Testing" project. That project defines the test protocol; this project provides the market context and tracking framework.
- Consider merging the two projects or having this one supersede the testing project's platform list (which only had 5 platforms, now expanded to 10).
- The portability testing project listed ChatGPT and Bolt as platforms. ChatGPT has been ruled out (stateless). Bolt remains but with uncertainty.

## Session Log

- 2026-02-09: Project created. Researched 10 platforms. PRD written and saved to docs/prd-agentic-platform-landscape.md. All tasks complete.
