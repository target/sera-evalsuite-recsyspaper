# Contributing

Thank you for your interest in contributing to SERA supplementary
materials.

## Development Setup

This repository contains static prompt and dataset artifacts. No build
step is required for normal editing.

Before opening a pull request, verify JSONL files are valid:

```sh
python3 - <<'PY'
import json, pathlib
for p in pathlib.Path("seed_datasets").glob("*.jsonl"):
    for i, line in enumerate(p.open(), 1):
        json.loads(line)
    print(f"ok {p}")
PY
```

## Contribution Guidelines

- Keep prompt files as plain text.
- Preserve the `A##_metric_name.txt` naming convention for metric prompts.
- Keep JSONL datasets one valid JSON object per line.
- Do not include private, proprietary, credential, or user-identifying data.
- Do not add production logs, traces, conversation IDs, internal tool names,
  retailer-owned brands, loyalty-program names, or private-system URLs.
- Use reserved namespaces and deliberately invalid values for synthetic PII.
- Do not add generated caches, local environment files, or editor metadata.
- Update `README.md` and `CHANGELOG.md` when adding or changing artifacts.

## Pull Requests

Pull requests should include:

- A short description of the change.
- The reason the change is needed.
- Any validation performed.
- Any compatibility impact on existing prompt or dataset consumers.

## Developer Certificate of Origin

This project uses Developer Certificate of Origin checks. By contributing,
you certify that you have the right to submit the contribution under this
project's license.
