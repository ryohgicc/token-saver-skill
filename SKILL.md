---
name: token-saver
description: Keep Codex token use low without slowing work by pre-compacting raw inputs, byte-capping command output, maintaining concise handoff notes, and inspecting only task-relevant snippets. Use for large repositories, logs, datasets, JSON/CSV dumps, long debugging sessions, quota-sensitive work, repeated agent handoffs, or any request where Codex might otherwise read broad raw data, verbose command output, generated folders, archives, or entire source files unnecessarily.
---

# Token Saver

## Core Rule

Prefer a small, task-shaped "needle map" over raw context. Before opening large or unknown inputs, create or request a compact summary that identifies the relevant files, time ranges, symbols, errors, entry points, decisions, and next actions.

## Workflow

1. Define the exact question before reading.
   - State the narrow target: bug location, date range, symbol, feature flow, failing test, config path, or decision needed.
   - Avoid broad prompts like "read this repo" or "analyze this file" when a targeted scan is possible.

2. Pre-compact raw data.
   - For logs, filter by timestamp, severity, keyword, request ID, symbol, or app component.
   - For CSV/JSON/data dumps, extract row counts, columns, samples, nulls, key stats, and top anomalies.
   - For repositories, build a repo map with entry points, configs, test commands, core flows, and generated/vendor directories to skip.
   - Feed the compact result into analysis first; inspect raw ranges only after the summary points to them.

3. Cap unknown output.
   - Any command with unknown or potentially large output should be limited by lines or bytes.
   - Use `head`, `tail`, `rg --max-count`, `git diff --name-only`, `git status --porcelain`, or `head -c`.
   - Write verbose output to a temp file, then inspect selected ranges or summaries.

4. Read snippets, not full files.
   - Locate the relevant function, type, error block, or config section with `rg`.
   - Show only the matching block plus a few lines of surrounding context.
   - Escalate to larger reads only when the snippet proves insufficient.

5. Maintain a living handoff.
   - For multi-turn or multi-agent work, keep a concise `HANDOFF.md` or equivalent under about 1k tokens.
   - Include current goal, success criteria, key files, decisions, commands run with outcomes, known issues, skip list, and next steps.
   - Periodically compact progress into the handoff and remove dead ends, repeated reasoning, and obsolete paths.

6. Set hard boundaries.
   - Skip dependencies, caches, builds, archives, generated outputs, large logs, and binary assets unless directly relevant.
   - Do not paste full source, raw logs, or full datasets unless explicitly requested.
   - Prefer summaries, diffs, and focused snippets in user-facing responses.

7. Keep responses concise.
   - Report the patch, result, or next action.
   - Do not restate unchanged plans.
   - Preserve detail for evidence, risks, and commands the user needs.

## When Creating Helpers

Create small reusable scripts when the same compaction would be useful again, such as:

- `repo_map.py` for entry points, configs, commands, and important directories.
- `compact_logs.py` for timestamp/keyword/severity slices and top anomalies.
- `scan_errors.py` for bounded error extraction.
- `summarize_json.py` or `summarize_data.py` for schema, counts, samples, and summary stats.

Keep helpers parameterized with `--limit`, `--since`, `--keyword`, `--symbol`, `--path`, or similar options. Test representative helpers once before relying on them.

## Reference Templates

Read `references/templates.md` when you need copy-ready command patterns, an `AGENTS.md` rule, handoff structure, or prompt templates for data-heavy tasks.
