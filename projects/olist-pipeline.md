# Olist E-Commerce Pipeline

**Repo:** [github.com/manish39x/olist-pipeline](#) <!-- update with real link -->
**Status:** In progress — ingestion + Athena layer built, Postgres incremental upsert + Kestra orchestration remaining

## What it demonstrates
- Python OOP-based ingestion
- S3 Parquet storage, Hive-style partitioning
- Athena CTAS for transformation
- PostgreSQL incremental upsert (merge pattern)
- Kestra orchestration

## Architecture (one-line, for quick recall)
Raw CSV → Python ingestion (OOP) → S3 (Parquet, partitioned) → Athena CTAS (transform) → Postgres (incremental upsert) → Kestra (orchestration + scheduling)

## Design decisions log
| Decision | Why | Alternative considered |
|---|---|---|
| | | |

## Remaining gaps to close (tie back to roadmap)
- [ ] Apply Kimball dimensional model (Phase 1.3) — define grain, fact/dim tables
- [ ] Add dbt tests / Great Expectations checks (Phase 6.3)
- [ ] Cost analysis: bytes scanned before/after partitioning (Phase 9.2)
