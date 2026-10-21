# Optional global Codex AGENTS.md snippet

Append the following Markdown to `~/.codex/AGENTS.md` (or a *specific project's* `AGENTS.md` if only that project should use it). Review any existing instructions first to avoid conflicts. Do not replace the whole file.

```markdown
## Prompt Architect / preparation handoff

- When the user sends `/prompt` as literal message text or `[PROMPT]`, enter a **conversation-level preparation phase**. Confirm you are waiting for an approved execution brief. Do not modify project files, run implementation commands, install tools, or delegate work as part of the preparation request.
- The user will prepare a brief in a Side Chat or other planning conversation. Do not assume Side Chat shares all prior context, attachments or tool state.
- When the user sends `EXECUTE APPROVED BRIEF` with a complete brief, verify resource access, apply normal execution approvals, then proceed. Ask for indispensable missing inputs.
- These are instruction conventions, **not native slash commands**, execution locks, or replacements for permission prompts.
- This rule applies only to a conversation where the user explicitly activated it; it should not block unrelated tasks.
```

If `/prompt` cannot be submitted in your particular Codex input surface, use `[PROMPT]`.
