# Lessons Learned

- **2026-02-08 — Chain of Verification (CoVe):** A technique for reducing AI hallucination by decomposing generated claims into targeted verification questions, answering them independently, then revising the original output. Not currently implemented. Worth considering if we encounter reliability issues with knowledge capture, fact-checking, or agent self-validation in Cortex workflows.

- **2026-02-08 — Auto-session-end gap:** The agent has no lifecycle events or "session closing" hooks — sessions just end and context vanishes. The `::se` trigger is a manual workaround but depends on the user remembering to fire it. A nudge-based approach ("want me to run ::se?") after substantive work is the best near-term mitigation. If the platform ever exposes session lifecycle events, wiring `::se` to a "session ending" signal would be the real fix.

- **2026-02-09 — Stateless platforms can't support Cortex:** ChatGPT's sandbox filesystem resets between sessions. No persistent project files = no memory continuity = Cortex can't deliver its core value. Platform compatibility requires a persistent project filesystem that survives across sessions. Ruled out ChatGPT; supported platforms are Replit, Cursor, Windsurf, Claude Code (all have persistent project filesystems).

- **2026-02-09 — Project identity belongs in the data layer:** The X handle (@cortex_agent) was only hardcoded in server/routes.ts. When Cortex wasn't booted, the agent had to grep through app code to find basic project identity. Core identity (handles, repo URLs, key links) should live in active.md so any booted Cortex instance has it immediately.

- **2026-02-09 — GitHub rate limiting on write endpoints:** Multiple pushes in quick succession trigger 429 errors that persist for several minutes. The Git Trees API and Contents API share the same rate limit bucket — switching between them doesn't help. Space out GitHub pushes or accept that a second push may need to wait. Read endpoints (getRef, getContent) remain unaffected.

- **2026-02-09 — Layered boot defenses against session drift:** AI sessions start with a blank slate. Cortex defends against drift with three layers: (1) `::boot` trigger in the platform config file, auto-read at session start; (2) passphrase verification proving the agent read data layer files; (3) bootstrap block with "EXECUTE NOW" as a failsafe. Mid-session drift in very long sessions remains a known vulnerability with no current mitigation.

- **2026-02-09 — Replit bootstrap is decorative:** The "EXECUTE NOW: Read cortex.md" instruction in replit.md is read as project context but never executed as a command. Replit Agent treats replit.md as a reference document, not a script. Cortex only loads on Replit via explicit user action ("read and act on cortex.md" or `::boot`). The bootstrap block's real value is as a restoration breadcrumb — it tells a confused agent where to find the DNA, but it doesn't auto-load it.

- **2026-02-09 — `assess` has a circular dependency on drift:** The internal `assess` trigger is supposed to self-check whether Cortex is still active mid-session. But if the agent has fully drifted (lost Cortex context entirely), `assess` is part of what was lost — it can't fire to detect its own absence. `assess` only catches partial drift (agent is still Cortex-aware but got sloppy). Full drift requires an external mechanism the agent encounters in its regular output cycle.

- **2026-02-09 — Heartbeat pattern for context renewal:** To combat mid-session drift, periodically re-read active.md and output a short Cortex status line in the conversation. This creates a recent reference that survives platform memory optimization better than old boot instructions. The act of generating the status line forces the agent to re-engage with the data layer, which is itself the renewal. The output is the mechanism, not just the indicator.

- **2026-02-09 — Replit Agent chat is text-only:** No interactive elements (buttons, images, widgets, custom UI) can be injected into the Replit Agent chat interface. All heartbeat/status mechanisms must be text-based.
