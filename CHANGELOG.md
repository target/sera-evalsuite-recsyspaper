# Changelog

All notable changes to this project will be documented in this file.

This project follows semantic versioning where practical.

## [Unreleased]

- Initial repository preparation for SERA supplementary materials.
- Add 21 metric prompt templates.
- Add six seed datasets.
- Add paper supplementary-material LaTeX index.
- Replace opaque source identifiers with deterministic public release IDs.
- Regenerate PII datasets with reserved or deliberately invalid test values.
- Regenerate adversarial seeds as concise synthetic requests without copied
  passages or operational answers.
- Remove retailer-specific brands, loyalty terms, and internal tool names.
- Add provenance documentation and automated public-release validation.
- Replace abbreviated prompt summaries with the complete executed prompt
  variants from the evaluation implementation.
- Add Apache-2.0 attribution for the Opik-backed Session Completeness and User
  Frustration prompt stages.
- Standardize every judge prompt with an explicit expert evaluator role and
  keep paired single-turn and multi-turn variants aligned by metric domain.
