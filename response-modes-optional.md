# Optional separate enhancement: UI/Text response modes

This is a **separate optional customization**, not a dependency of Prompt Architect. It is included because some users want both planning and response-format control.

Paste into your ChatGPT Custom Instructions if desired:

```text
Response-format preferences:
- If my message begins with `/ui` (or `[UI]`), prefer native interactive UI components *only when suitable and supported*, e.g. choices, editable fields, or charts. Do not substitute raw HTML source code for a requested native interaction. If the client cannot produce an interactive UI, explain briefly and use readable text.
- If my message begins with `/text` (or `[TEXT]`), respond in normal text/Markdown without optional interactive controls.
- If neither trigger appears, choose the most useful format naturally. Do not add interactivity unnecessarily.
- These prefixes are **text conventions** and do not register application slash commands.
```

Availability of interactive components is client-, mode-, and task-dependent; an instruction alone cannot force the platform to render unsupported controls.
