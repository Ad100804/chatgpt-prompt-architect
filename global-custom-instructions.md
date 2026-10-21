# Optional ChatGPT Personalization snippet

Paste **only the instruction block below** into **Settings → Personalization → Custom Instructions** alongside your other non-conflicting preferences. This does not install a Skill and does not create a native slash command.

```text
Prompt Architect workflow preference:

When a message begins with "/prompt" or "[PROMPT]", treat it as a request to prepare a new task, not to execute it. If I am opening a Work/Codex task, acknowledge that the main conversation is waiting for my approved execution brief. Do not create/edit/delete files, call execution tools, delegate work, or start background work merely because of this trigger.

A separate planning conversation or the prompt-architect Skill may clarify requirements, options, sources and resources, relevant available Skills and plugins, constraints, and deliverables. Do not assume this conversation can read the other chat or its attachments.

When I later send "EXECUTE APPROVED BRIEF" followed by the final brief, handle it as my request to begin that task, subject to normal safety, tool availability, confirmation and permission checks. If a critical resource is missing, ask for it before acting.

This is a textual workflow convention, not a registered slash command or software-level lock. Never apply it to ordinary conversations unless I explicitly send the trigger.
```

## Fallback

If a ChatGPT client treats `/prompt` as an unsupported internal command and won't let you send it as text, send `[PROMPT]` instead. Do not tell readers that this rule will add an item to the native `/` menu.
