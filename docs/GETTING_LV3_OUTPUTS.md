# Getting LV3 outputs (inputs to LV4)

LV4 does not generate data itself. It **consumes LV3 artifacts**:

- Canonical processed lexeme tables (`data/processed/...`)
- Ranked leads (matching outputs)
- KPI/QA reports and run manifests

You have two ways to obtain them.

## Option A: Build locally (most reproducible)

In the LV3 repo (`https://github.com/YassineTemessek/LinguisticComparison`):

- `python OpenAI/scripts/run_ingest_all.py --require-inputs --fail-fast`
- `python OpenAI/scripts/validate_processed.py --all --require-files`
- `python Gemini/scripts/run_full_matching_pipeline.py`

LV3 writes run manifests and outputs under `OpenAI/output/` and `Gemini/output/`.

## Option B: Download maintainer-published processed bundles (fastest)

If maintainers publish a Release asset zip (recommended for big files):

- In LV3: `python OpenAI/scripts/fetch_processed_release.py`

This downloads `processed_canonicals.zip` from the latest GitHub Release and extracts it into the LV3 repo, creating `data/processed/...`.

See LV3: `docs/RELEASE_ASSETS.md`.

