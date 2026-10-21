# ChatGPT Prompt Architect

**Turn messy ideas into clear, structured execution briefs—without leaving your AI workspace.**

[简体中文说明 / Chinese guide](docs/README.zh-CN.md)

> Community-made, instruction-first project for ChatGPT and Codex. Not affiliated with or endorsed by OpenAI. This is **not** a standalone application, browser extension, or an officially registered `/prompt` command.

## The problem

A task often starts with incomplete thoughts: "Improve my slide deck," "Add multiplayer to my game," or "Research this topic." A one-shot prompt improver can rewrite wording, but may not discover missing decisions, available resources, tool limitations, or clear acceptance criteria.

**Prompt Architect** is a reusable planning skill designed to conduct that conversation *inside your existing ChatGPT workflow* before handing a self-contained execution brief to a separate Work or Codex task.

## Why use an in-ChatGPT workflow?

| In-ChatGPT planning | Typical external prompt-rewriting tool |
|---|---|
| Can use context that the current conversation or project actually exposes | Usually requires manual copy-paste of context |
| Can ask follow-up questions and revise the brief over multiple turns | Often focuses on one-shot rewriting |
| Can *recommend* Skills, plugins, MCP and native tools and check their availability when accessible | Usually doesn't know which tools are available in the target session |
| Makes it easy to move a brief to ChatGPT Work or Codex | Requires switching apps before execution |
| Keeps a transparent source/resource manifest with stable IDs | May output only a block of rewritten prose |

**Important limits:** A Side Chat does not guarantee complete or live access to the main chat. Attachments, permissions, tool state, ChatGPT Memory, and selected plugins do not necessarily transfer to another conversation. The final prompt therefore includes explicit resource references and verification steps. ChatGPT Work and Codex still have separate capabilities. No command here can force the desktop client to expose features it does not support.

## What the workflow does

1. **Understand** an informal request; identify goals, scope, and intended target (Chat / Work / Codex).
2. **Inventory** sources, attachments, working files, installed or suggested Skills, plugins and tools.
3. **Explore** 2–3 viable interpretations when choices meaningfully affect the outcome.
4. **Clarify** only important unanswered questions; the user may answer in natural language or by ID.
5. **Produce** a copyable **Structured Execution Brief**, including acceptance criteria and verification instructions.
6. **Execute separately:** the user explicitly pastes/approves the final brief in the main task conversation.

Planning does not edit project files or run implementation steps.

## Reference ID system

| Prefix | Category | Example |
|---|---|---|
| `S01` | Sources / evidence | Assignment rubric or official documentation |
| `R01` | Resources / assets | Uploaded screenshot or local repository |
| `K01` | Skills | `prompt-architect` or another verified Skill |
| `P01` | Plugins, MCP, external tools | GitHub MCP (if actually available) |
| `C01` | Constraints | Do not edit unrelated slides |
| `O01` | Options | Minimal changes vs balanced redesign |
| `Q01` | Questions | Which files are authoritative? |
| `D01` | Deliverables | Updated `.pptx` and change summary |

IDs remain stable across revisions. You can answer **`O02; Q01: pages 3–7 only; Q02: preserve annotations; remove P01`**.

## Quick start

### A. Use the Prompt Architect Skill

The main skill is at [`skills/prompt-architect/SKILL.md`](skills/prompt-architect/SKILL.md). You can create/import it with your supported ChatGPT Skills workflow (e.g. `@skill-creator` in Work) or place it in Codex's user skills folder:

```bash
mkdir -p ~/.agents/skills/prompt-architect
cp skills/prompt-architect/SKILL.md ~/.agents/skills/prompt-architect/SKILL.md
```

Open ChatGPT desktop and select the installed Skill when available (`@prompt-architect` in a supported ChatGPT surface, `$prompt-architect` in supported Codex workflows). Availability depends on the client and the Skill's installation method. See [OpenAI's Skills guide](https://learn.chatgpt.com/docs/build-skills).

**No installation required to test:** copy the content of `SKILL.md` into a planning conversation as instructions, then describe your task. This is a manual prompt, not a registered Skill.

### B. Optional `/prompt` preparation shorthand

Add the instructions from [`instructions/global-custom-instructions.md`](instructions/global-custom-instructions.md) to **Settings → Personalization → Custom Instructions** for Chat/Work guidance. For Codex, append the relevant rules from [`instructions/codex-AGENTS-snippet.md`](instructions/codex-AGENTS-snippet.md) to your own `~/.codex/AGENTS.md` after checking for conflicts.

Then create a main task chat and send:

```text
/prompt
```

If `/prompt` is interpreted as an unknown *native* slash command, use:

```text
[PROMPT]
```

These are **text triggers** described in your instructions, not registered application slash commands, and they are not hard execution locks. The optional [`prompt-start`](skills/prompt-start/SKILL.md) Skill is a second way to request the same behavior in supported clients.

### C. Plan in a Side Chat (if available) or separate chat

**Main task chat:** Send the preparation trigger and wait for acknowledgement. 

**Planning chat:** Invoke Prompt Architect, then give a rough idea:

```text
I want to improve my Three.js FPS game's multiplayer experience.
I have not decided on architecture, testing, or acceptance criteria.
Please clarify the requirements, inventory verified resources,
and suggest only relevant Skills and plugins. Do not implement anything.
```

**Planning responses:** Review `S/R/K/P/C/O/Q/D` IDs, answer questions, and choose options.

**Finalize:** Say `Finalize the execution brief`.

**Main task chat:** Paste the approved brief beginning with:

```text
EXECUTE APPROVED BRIEF
```

If Side Chat is missing or context transfer is incomplete, use a separate Chat session and include required background and attachments explicitly. For Work, planning in Chat first is often simpler than starting a Work task just to put it on hold.

## Sample result

See [`examples/affinity-slideshow.md`](examples/affinity-slideshow.md) for a hypothetical planning round; the copyable final format is in [`templates/execution-brief.md`](templates/execution-brief.md).

## Package layout

```text
chatgpt-prompt-architect/
├── README.md
├── LICENSE
├── .gitignore
├── skills/
│   ├── prompt-architect/SKILL.md
│   └── prompt-start/SKILL.md
├── instructions/
│   ├── global-custom-instructions.md
│   ├── codex-AGENTS-snippet.md
│   └── response-modes-optional.md
├── templates/execution-brief.md
├── examples/affinity-slideshow.md
└── docs/README.zh-CN.md
```

## Safety, correctness, and honest boundaries

- Do not include private files, real API keys, auth tokens, or personal ChatGPT memories in a public repository.
- Do not claim a Skill or plugin is installed unless it was verified in the current environment.
- An ID is a label, not proof that a named file or reference is accessible.
- `/prompt` and `EXECUTE APPROVED BRIEF` are **behavioral conventions** only; always review approvals and tool permissions.
- Planning may inspect supplied sources with read-only tools when appropriate, but must not make project changes or install dependencies.
- A copyable brief is not guaranteed to carry files or live app connections into a new chat.

## Status and roadmap

**v0.1.0 — initial public template (not yet independently validated on every client).**

Potential improvements: richer Work/Codex templates, better portability, optional interactive planning widgets, and a distributable plugin package. Contributions and corrections are welcome.

## License

MIT — see [LICENSE](LICENSE).
