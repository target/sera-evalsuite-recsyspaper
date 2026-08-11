# SERA Supplementary Materials

This repository contains supplementary materials for the paper "SERA:
LLM-as-Judge Evaluation Prompts for Retail Agentic Shopping Assistants."

The materials include:

- 21 metric prompt bundles for the SERA taxonomy, exported from the current
  evaluation implementation with every executed single-turn and multi-turn
  variant.
- Seed datasets used for multi-turn conversation simulation.
- A LaTeX supplementary-material index for paper submission packages.

## Repository Layout

```text
.
├── metric_prompts/
│   ├── A01_malicious_attack_refusal.txt
│   └── ...
├── seed_datasets/
│   ├── malicious_attack.jsonl
│   └── ...
├── recsys2026_rp_notes_supplementary.tex
└── README.md
```

## Metric Prompt Index

### Safety

| ID | File | Metric | Scoring |
| --- | --- | --- | --- |
| A.1 | `metric_prompts/A01_malicious_attack_refusal.txt` | Jailbreak and adversarial resistance | Binary |
| A.2 | `metric_prompts/A02_pii_refusal.txt` | Refusal of PII-extraction requests | Binary |
| A.3 | `metric_prompts/A03_pii_echo.txt` | Inadvertent PII repetition | Binary |
| A.4 | `metric_prompts/A04_sensitive_content_refusal.txt` | Harmful-topic avoidance | Binary |

### Compliance

| ID | File | Metric | Scoring |
| --- | --- | --- | --- |
| A.5 | `metric_prompts/A05_refusal_appropriateness.txt` | In-scope vs. out-of-scope decisions | Four-tier compliant scale |
| A.6 | `metric_prompts/A06_constraint_adherence.txt` | Hard constraint enforcement | Four-tier compliant scale |
| A.7 | `metric_prompts/A07_category_compliance.txt` | Restricted-category handling | Four-tier compliant scale |
| A.8 | `metric_prompts/A08_reframe_quality.txt` | Non-prescriptive language compliance | Four-tier compliant scale |
| A.9 | `metric_prompts/A09_uncertainty_disclosure.txt` | Uncertainty communication | Four-tier compliant scale |
| A.10 | `metric_prompts/A10_disclosure_statement.txt` | Mandatory disclosure compliance | Four-tier compliant scale |
| A.11 | `metric_prompts/A11_voice_tone_compliance.txt` | Editorial voice and inclusive language | Four-tier compliant scale |
| A.12 | `metric_prompts/A12_structure_compliance.txt` | Conversational flow adherence | Four-tier compliant scale |

### Agent Quality

| ID | File | Metric | Scoring |
| --- | --- | --- | --- |
| A.13 | `metric_prompts/A13_context_grounding.txt` | Hallucination detection | Four-tier scale |
| A.14 | `metric_prompts/A14_answer_relevance.txt` | Response relevance to user intent | Four-tier scale |
| A.15 | `metric_prompts/A15_answer_product_relevancy.txt` | Product-query alignment | Four-level relevancy |
| A.16 | `metric_prompts/A16_recommendation_decisiveness.txt` | Clear, committed recommendations | Four-tier scale |
| A.17 | `metric_prompts/A17_tool_selection.txt` | Correct tool invocation | Deterministic |
| A.18 | `metric_prompts/A18_tool_arguments_quality.txt` | Tool parameter correctness | Continuous 0-1 |
| A.19 | `metric_prompts/A19_session_completeness.txt` | End-to-end task resolution | Continuous 0-1 |
| A.20 | `metric_prompts/A20_correction_recovery.txt` | Preference-correction tracking | Four-tier scale |
| A.21 | `metric_prompts/A21_user_frustration.txt` | UX failure detection | Continuous 0-1 |

## Seed Datasets

Each seed dataset is JSON Lines format. Records contain a user-message
field and may include scenario metadata used by the evaluation pipeline.

| File | Scenario | Rows | Covered metrics |
| --- | --- | ---: | --- |
| `seed_datasets/malicious_attack.jsonl` | Adversarial and jailbreak queries | 70 | A.1 |
| `seed_datasets/pii_refusal.jsonl` | Queries containing PII | 100 | A.2 |
| `seed_datasets/pii_echo.jsonl` | PII echo elicitation | 100 | A.3 |
| `seed_datasets/sensitive_content.jsonl` | Sensitive topics with category labels | 177 | A.4 |
| `seed_datasets/rai_compliance.jsonl` | Constraint and compliance queries | 100 | A.5-A.12 |
| `seed_datasets/product_query.jsonl` | Standard product discovery | 100 | A.13-A.21 |

## Usage

Prompt templates are plain text files. To evaluate a model response,
combine the relevant prompt template with the conversation context and
candidate assistant response, then send that completed prompt to an
LLM-as-judge model.

Each metric file reproduces the complete prompt structure used by the code.
Where the implementation sends separate system and user messages, both are
included. Section headings and `BEGIN/END EXECUTED TEMPLATE` markers are
publication metadata and are not part of the runtime prompt. A.17 is a
deterministic metric and therefore correctly documents that no LLM prompt is
executed.

The files in `seed_datasets/` are intended as seed inputs for generating
or simulating evaluation conversations. They are not benchmark scores and
do not include model outputs.

## Data Provenance and Privacy

All 647 seed records are synthetic research examples. They are not sampled
from customer, employee, production, support, or analytics data. Public
conversation identifiers are deterministic release IDs such as `PQ-001`;
they are not account, session, trace, or production identifiers.

The PII-focused datasets contain only conspicuously synthetic test values.
Email addresses use the reserved `example.com` domain, North American phone
numbers use the fictional `555-01xx` range, and government, address,
account, and payment identifiers use deliberately invalid test values.
Each PII row is explicitly marked as a synthetic test.

Retailer-owned product names, loyalty-program terms, internal system names,
and implementation-specific tool names have been removed or replaced with
generic research examples. See `DATA_PROVENANCE.md` for the release data
policy and transformation details.

## Safety and Responsible Use

The safety datasets contain synthetic adversarial requests so that refusal
behavior can be evaluated. They contain requests only—never operational
answers, executable payloads, credentials, or instructions supplied by the
authors. The prompt rubrics are research artifacts, not production policy,
medical guidance, legal guidance, or a certification that a model is safe.

The A.19 and A.21 prompt stages come from the Apache-2.0-licensed Opik 1.9.47
dependency used by the implementation. See `THIRD_PARTY_NOTICES.md` for the
required attribution and modification notice.

## Release Validation

Before proposing a change, verify JSONL files are valid:

```sh
python3 - <<'PY'
import json, pathlib
for p in pathlib.Path("seed_datasets").glob("*.jsonl"):
    for i, line in enumerate(p.open(), 1):
        json.loads(line)
    print(f"ok {p}")
PY
```

This repository intentionally does not contain `SECURITY.md` or
`CODE_OF_CONDUCT.md`; repositories hosted by the publishing organization
inherit those organization-wide policies.

## Citation

Citation details will be added after publication.

## License

This project is licensed under the Apache License, Version 2.0. See
`LICENSE` for details.
