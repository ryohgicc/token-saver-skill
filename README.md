# Token Saver Skill

Token Saver is a Codex skill for keeping large tasks lean. It teaches Codex to pre-compact raw inputs, cap command output, inspect focused snippets, and maintain concise handoff notes before reading broad logs, datasets, or repositories.

## What It Helps With

- Large repositories where reading every file would waste context.
- Logs, JSON, CSV, or other raw data dumps.
- Long debugging sessions that need a compact project memory.
- Quota-sensitive Codex work where token discipline matters.
- Repeated handoffs between sessions or agents.

## Install

Clone or copy this repository into your Codex skills directory:

```bash
mkdir -p ~/.codex/skills
git clone https://github.com/ryohgicc/token-saver-skill.git ~/.codex/skills/token-saver
```

Restart Codex or start a new session so the skill list refreshes.

## Usage

Invoke the skill explicitly when a task may involve large context:

```text
Use $token-saver to inspect this large repo and build a compact repo map before changing code.
```

```text
Use $token-saver to analyze this log file. First create a needle map under 500 tokens, then inspect only the relevant ranges.
```

```text
Use $token-saver to keep this debugging session compact and maintain a HANDOFF.md as we go.
```

Codex may also trigger it implicitly for tasks involving large repositories, verbose command output, logs, datasets, generated files, archives, or repeated handoffs.

## Core Workflow

1. Define the exact question before reading.
2. Create a compact needle map from raw inputs.
3. Cap unknown command output by bytes or lines.
4. Read snippets instead of full files.
5. Maintain a short `HANDOFF.md` for long-running work.
6. Skip dependencies, caches, generated files, archives, and binary assets unless directly relevant.
7. Keep responses concise and focused on results.

## Included Templates

The skill includes copy-ready templates in `references/templates.md`:

- Safe command output patterns.
- Git inspection commands.
- Data and log inspection commands.
- Helper script briefs.
- `HANDOFF.md` structure.
- `AGENTS.md` command-output-protection rule.
- Prompt templates for data-heavy tasks.

## Repository Layout

```text
.
├── SKILL.md
├── agents/
│   └── openai.yaml
└── references/
    └── templates.md
```
