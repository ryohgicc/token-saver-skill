# Token Saver Templates

## Command Output Protection

Use byte or line caps on unknown output:

```bash
COMMAND 2>&1 | head -c 6000
head -n 80 path/to/file
tail -n 80 path/to/file
rg -n "KEYWORD" path/to/file | head -n 40
```

Write verbose output to a temp file, then inspect bounded ranges:

```bash
python analyze.py > /tmp/analysis.txt 2>&1
head -c 8000 /tmp/analysis.txt
sed -n '120,220p' /tmp/analysis.txt
```

## Git Commands

```bash
git status --porcelain | head -n 30
git log --oneline -15
git diff --name-only | head -n 20
git diff -- path/to/file | head -c 12000
```

## Data And Log Commands

```bash
tail -n 200 app.log | rg "ERROR|WARN" | head -n 50
jq 'keys' data.json | head -c 4000
python -c "import pandas as pd; df = pd.read_csv('data.csv'); print(df.head(20).to_string()); print(df.describe(include='all').to_string())" | head -c 10000
```

## Helper Script Briefs

Ask Codex to create helpers with bounded output:

- `compact_logs.py`: Filter by timestamp, severity, keyword, component, or ID; print top N anomalies and examples.
- `summarize_data.py`: Print file size, schema, row count, column summaries, sample rows, missing values, and outliers.
- `repo_map.py`: Print entry points, configs, package managers, test commands, core modules, and skip directories.
- `scan_errors.py`: Print distinct errors with counts, first/last timestamps, and capped examples.

## Handoff Template

```markdown
# HANDOFF

## Current Goal

## Success Criteria

## Key Files

## Decisions

## Commands Run

## Known Issues

## Do Not Re-read

## Next Steps
```

Keep it under about 1k tokens. Remove repeated reasoning, failed paths, and stale details.

## AGENTS.md Rule

```markdown
## Command Output Protection

Any command with unknown or potentially large output MUST be byte-capped.
Default: `COMMAND 2>&1 | head -c 6000`.
If more is needed, write to a temp file and inspect selected ranges only.

Skip dependency folders, virtual environments, build output, generated files,
cache directories, archive logs, and binary assets unless directly relevant.
Summarize before opening new large files. Never paste full source or raw data
unless explicitly requested.
```

## Prompt Templates

```text
First create a <500-token needle map from the raw input, then analyze only that.
Do not read the raw file directly unless the needle map identifies a specific range.
```

```text
Locate the relevant function or config. Show only that block plus 3 lines above
and below, then explain the edge case in one paragraph.
```

```text
Build a one-page repo map: entry points, config, main data flows, test commands,
and directories to skip. Avoid vendor, generated, build, cache, and archive dirs.
```
