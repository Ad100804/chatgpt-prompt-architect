---
name: prompt-start
description: Put a new Codex or Work task conversation into a user-defined preparation-only state while a separate planning chat refines the requirements. Invoke only when the user explicitly requests prompt preparation or a waiting mode.
---

# Prompt Start — preparation-only handoff

When explicitly invoked to start a planning-first task, do not begin the substantive task, edit files, run commands, install plugins, delegate, or start background jobs. Briefly acknowledge that this conversation will await an approved execution brief.

Suggested acknowledgement:

> Preparation mode ready. I will not begin the task yet. Use Prompt Architect in a Side Chat (if available) or separate planning chat. Return with the approved execution brief.

A final user message headed `EXECUTE APPROVED BRIEF` signals that they wish to proceed. Verify prerequisites and apply normal security and permission checks. This is **not a software-level execution lock**; an instruction-only Skill cannot enforce permission controls. Do not assume a Side Chat shares all main-chat context or that it has finished unless the user says so.
