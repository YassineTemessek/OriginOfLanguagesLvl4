# Getting LV3 outputs (inputs to LV4)

LV4 does not generate data itself. It **consumes LV3 artifacts**:

- Canonical processed lexeme tables (`data/processed/...`)
- Ranked leads (matching outputs)
- KPI/QA reports and run manifests

You have two ways to obtain them.

## Option A: Build locally (most reproducible)

In the LV3 repo (`https://github.com/YassineTemessek/LinguisticComparison`):

- `python scripts/ingest/run_ingest_all.py --require-inputs --fail-fast`
- `python scripts/ingest/validate_processed.py --all --require-files`
- `python scripts/discovery/run_discovery_retrieval.py --source ... --target ...` (SONAR/CANINE retrieval + hybrid scoring)
- Optional legacy matcher: `python scripts/discovery/run_full_matching_pipeline.py`

LV3 writes run manifests, caches, and outputs under `outputs/`.

Note: SONAR/CANINE runs require the optional LV3 dependencies (`requirements.embeddings.txt`) and will download model weights on first use.

## Option B: Download maintainer-published processed bundles (fastest)

If maintainers publish a Release asset zip (recommended for big files):

- In LV3: `python scripts/ingest/fetch_processed_release.py`

This downloads `processed_canonicals.zip` from the latest GitHub Release and extracts it into the LV3 repo, creating `data/processed/...`.

See LV3: `docs/RELEASE_ASSETS.md`.
