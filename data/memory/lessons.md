# Lessons Learned

- **2026-02-08 — Chain of Verification (CoVe):** A technique for reducing AI hallucination by decomposing generated claims into targeted verification questions, answering them independently, then revising the original output. Not currently implemented. Worth considering if we encounter reliability issues with knowledge capture, fact-checking, or agent self-validation in Cortex workflows.

- **2026-02-08 — Auto-session-end gap:** The agent has no lifecycle events or "session closing" hooks — sessions just end and context vanishes. The `::se` trigger is a manual workaround but depends on the user remembering to fire it. A nudge-based approach ("want me to run ::se?") after substantive work is the best near-term mitigation. If the platform ever exposes session lifecycle events, wiring `::se` to a "session ending" signal would be the real fix.
