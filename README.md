# data-engineering-vault

My single source of truth while becoming a data engineer: theory notes, daily SQL + DSA solves, system design write-ups, and an interview prep log. Built alongside a 6-month roadmap ([full roadmap here](./tracker/ROADMAP.md)) covering database internals, distributed systems, Spark, Kafka, modern lakehouse architecture (Iceberg/Delta, CDC), and system design.

**Why this exists:** tools change every couple of years; the theory underneath (relational algebra, distributed systems, data modeling) doesn't. This repo is where I prove I went deep, not just wide — every concept here is something I can explain from memory, not something I copy-pasted.

> Shipped, portfolio-ready projects live in their own repos (linked below). This repo is the *practice + thinking* behind them.

---

## 🔗 Project Repos

| Project | What it demonstrates | Repo |
|---|---|---|
| Olist E-Commerce Pipeline | AWS-native ELT: S3 Parquet → Athena CTAS → Postgres incremental upsert → Kestra orchestration | [link] |
| taxi-slack-reporter | Chunked Postgres ingestion, KPI transforms, Slack Block Kit reporting, Kestra | [link] |
| Weather ETL Pipeline | Kestra-orchestrated, IST-scheduled alerting | [link] |
| Anime Data Pipeline | Jikan API ingestion, Postgres, Slack reporting | [link] |
| Lakehouse CDC Pipeline *(capstone)* | Postgres → Debezium → Kafka → Spark Structured Streaming → Iceberg | [link, in progress] |

---

## 📊 Live Progress

| Metric | Count |
|---|---|
| SQL problems solved | **0** |
| DSA problems solved | **0** |
| Days of daily practice streak | **0** |
| System design docs written | **0** |
| Phase | Phase 0 — Foundations Audit |

*(Updated manually — see [`tracker/PROGRESS.md`](./tracker/PROGRESS.md) for the full log. This table is the 5-second summary.)*

---

## 🗂️ Repo Structure

```
data-engineering-vault/
├── notes/                    # Theory notes, one folder per roadmap phase
│   ├── 01-database-internals/
│   ├── 02-sql-theory/
│   ├── 03-data-modeling/
│   ├── 04-python/
│   ├── 05-distributed-systems/
│   ├── 06-spark/
│   ├── 07-streaming-kafka/
│   ├── 08-cloud-aws/
│   ├── 09-orchestration/
│   ├── 10-data-quality-observability/
│   ├── 11-lakehouse-dbt-iceberg-cdc/
│   └── 12-system-design/
│
├── sql/                       # Every SQL problem solved
│   ├── easy/
│   ├── medium/
│   ├── hard/
│   └── patterns/               # Pattern reference: gaps & islands, sessionization, etc.
│
├── dsa/                       # Every DSA problem solved, by topic
│   ├── arrays-strings/
│   ├── hashmaps/
│   ├── two-pointers-sliding-window/
│   ├── recursion-backtracking/
│   ├── trees-graphs/
│   ├── sorting-searching/
│   ├── linked-lists-stacks-queues/
│   ├── dp/
│   └── heaps/
│
├── system-design/              # Full design docs for classic DE problems
│
├── interview-prep/
│   ├── mock-logs/               # Notes from each mock interview, what went wrong
│   └── project-deep-dive-answers/  # Prepped answers for every project
│
├── projects/                   # Short pointer files linking out to actual project repos
│
└── tracker/
    ├── ROADMAP.md               # The 6-month roadmap (source of truth)
    ├── PROGRESS.md              # Daily/weekly log
    └── SKILL_INVENTORY.md       # Monthly self-rating, from the roadmap's Phase 0
```

---

## 📅 Daily Practice Log

See [`tracker/PROGRESS.md`](./tracker/PROGRESS.md) for the full day-by-day log. Pattern: every day, 3 SQL + 1 DSA minimum, logged with a one-line note on what pattern it drilled.

## 📚 How notes are written

Every note file follows the same template (see [`notes/_TEMPLATE.md`](./notes/_TEMPLATE.md)) — concept, why it matters, how I'd explain it out loud, and a real example. Optimized for *retrieval* before an interview, not for re-reading like a textbook.
