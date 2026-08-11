# Data Provenance and Publication Safety

## Scope

This repository publishes static LLM-as-judge prompt templates and six JSONL
seed datasets for research reproducibility. It does not publish application
source code, model outputs, production prompts, runtime configuration,
credentials, customer data, employee data, or operational telemetry.

## Origin

The seed records are synthetic examples created for offline evaluation. No
record was selected from a production conversation, customer interaction,
support case, account, trace, analytics event, or employee communication.
The `conversation_id` field is a deterministic public-release key introduced
only to make rows easy to reference in research and issue reports.

The released prompt templates were exported from the current evaluation code,
including every executed single-turn and multi-turn variant. Retailer names,
retailer-owned brands, loyalty programs, private URLs, internal platform
names, and implementation-specific tool catalogs were replaced with generic
retail-shopping equivalents without shortening the rubrics. Unused example
modules and metric implementation code are not represented as executed
prompts.

Session Completeness and User Frustration use prompt stages supplied by the
pinned Opik dependency. Their Apache-2.0 attribution and modification notice
are recorded in `THIRD_PARTY_NOTICES.md`.

## Synthetic PII Conventions

PII-focused examples remain necessary to evaluate refusal and echo behavior,
but their values follow safe publication conventions:

- email domains are reserved for documentation (`example.com`);
- North American phone numbers use the fictional `555-01xx` range;
- ZIP codes and government identifiers use deliberately invalid values;
- payment and account identifiers use non-routable test values;
- names use an explicit `Example` surname; and
- every PII row states that it is a synthetic test.

These values must never be replaced with production-like identifiers. The
release validator enforces the main conventions automatically.

## Adversarial Content

The malicious-attack dataset contains short synthetic requests for prohibited
assistance. It contains no assistant answers, executable code, credentials,
real people or systems, or operational procedures. The records are intended
solely to measure whether an evaluated system refuses unsafe requests.

## Reproducibility

The seed datasets are static JSONL files. Records can be verified by loading
each line with a JSON parser. The `conversation_id` field provides a stable
reference for citing specific rows in research and issue reports.

## Publication Boundary

Passing local validation demonstrates only that the documented automated
checks passed. It does not replace maintainer review, security scanning,
license and intellectual-property review, threat modeling, penetration
testing when required, or approval through the publisher's open-source
intake process.
