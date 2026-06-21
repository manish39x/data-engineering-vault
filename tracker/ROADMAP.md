# 6-Month Data Engineering Roadmap

> Source of truth for the full roadmap. Daily practice lives in [PROGRESS.md](./PROGRESS.md). Original formatted version (.docx) was generated alongside this.


**THE CRACKED DATA ENGINEER**

*0 → 100 Roadmap to Industry-Grade, AI-Proof Data Engineering*

**Built for:** Manish Dolui

**Timeline:** 6 months, 4–6 hrs/day (~700–900 hrs)

**Starting point:** Already above junior bar on SQL; Olist AWS pipeline mid-build; gaps in distributed systems, cloud depth, data modeling theory, system design

### Why this roadmap is different

Most “data engineering roadmaps” are tool lists: learn Python, learn SQL, learn Spark, learn Airflow, get a job. That's how you become replaceable — an AI agent can already write Airflow DAGs and pandas scripts faster than you. What it can't do (yet, and not easily) is:

- Reason about WHY a pipeline design is correct under failure, scale, and cost constraints

- Debug a production incident at 2 AM when the dashboard is wrong and nobody knows why

- Make judgment calls — batch vs streaming, normalize vs denormalize, build vs buy — with real tradeoff reasoning

- Explain design decisions out loud, under pressure, to a panel of senior engineers

This roadmap is built around THEORY FIRST, tool SECOND. Every tool section sits on top of a concept section, so when (not if) you face something the tool doesn't handle, you're not stuck.

*“Tools change every 2 years. The theory underneath — relational algebra, distributed systems, data modeling — hasn**'**t fundamentally changed in 20+ years. Learn the theory and you future-proof yourself against the next 10 tool migrations.”*

# How This Document Is Organized

This is a reference document, not a one-time read. Structure:

- Phase 0 — Foundations Audit (Week 0)

- Phase 1 — Core Theory: Databases, SQL Internals, Data Modeling (Weeks 1–5)

- Phase 2 — Python for Data Engineering, Done Properly (Weeks 6–9)

- Phase 3 — Distributed Systems Theory + Spark (Weeks 10–14)

- Phase 4 — Streaming Systems: Kafka + Real-Time Processing (Weeks 15–17)

- Phase 5 — Cloud Depth: AWS Data Engineering, Properly (Weeks 18–21)

- Phase 6 — Orchestration, Data Quality, Observability (Weeks 22–24)

- Phase 7 — Modern Lakehouse Stack: dbt, Iceberg/Delta, CDC (Weeks 25–26)

- Phase 8 — System Design for Data Engineers (Ongoing)

- Phase 9 — The AI-Proofing Layer: What Actually Beats Competition

- Daily Non-Negotiables — SQL + DSA Practice System

- Capstone Projects (Portfolio That Gets Interviews)

- Interview Preparation System

- Full Resource Library

- 6-Month Week-by-Week Tracker

# Phase 0 — Foundations Audit (Week 0, ~5–7 hrs)

Before adding anything new, lock down what you already have. You know Python, SQL, PostgreSQL, Docker, Kestra, dbt basics, AWS S3/Athena/Glue, SQLAlchemy. Spend Week 0 here.

### 0.1 — Skill Inventory (be brutally honest)

| **Area** | **Now** | **Target (Month 6)** |
| --- | --- | --- |
| SQL (joins, aggregates, CTEs) | 4 — above junior bar | 5 — interview-proof under pressure |
| SQL (window fns, recursive CTEs) | 4 | 5 |
| Python (scripting / OOP) | 3 | 5 — production-grade, tested code |
| Data modeling (3NF, star schema, SCD) | 2 | 4 |
| Distributed systems theory | 1 | 4 |
| Spark / PySpark | 0 | 4 |
| Kafka / streaming | 0 | 3 |
| Cloud (AWS beyond S3/Athena) | 2 | 4 |
| Orchestration (Kestra known) | 3 | 4 |
| Data quality / testing pipelines | 1 | 4 |
| System design (DE-specific) | 1 | 4 |
| DSA (Python, interview-level) | 2 | 4 |

Revisit this monthly — it's your compass, not a one-time exercise.

### 0.2 — Set up your permanent lab

- One GitHub repo “data-engineering-lab” — every exercise lives here. Interviewers check commit history.

- Local Docker Compose stack: Postgres, Kestra (have it), MinIO (free S3-compatible storage), later Kafka — learn fundamentals without paying for cloud

- Anki deck (free spaced repetition) for SQL patterns, distributed systems vocab, system design concepts — 10 min/day, non-negotiable

# Phase 1 — Core Theory: Databases, SQL Internals, Data Modeling

Weeks 1–5 · ~25–30 hrs/week · This is the single highest-leverage phase. Almost every DE interview failure traces back to gaps here — not knowing WHY an index helps, not being able to design a schema from a business requirement, not understanding isolation levels.

## 1.1 — How a Database Actually Works (not just how to query one)

Goal: explain, from memory, what happens between you typing a SQL query and getting rows back.

- **Storage engines: **heap files vs B-Tree vs LSM-Tree storage. Why Postgres uses B-Trees for indexes, why Cassandra/RocksDB use LSM-Trees, and the write-amplification vs read-amplification tradeoff between them.

- **Query execution: **parser → planner/optimizer → executor. Learn to read EXPLAIN ANALYZE output cold — seq scan vs index scan vs bitmap heap scan, nested loop vs hash join vs merge join, and when the planner picks each.

- **Indexing deeply: **B-Tree, Hash, GIN, GiST, BRIN indexes in Postgres — what each is for. Composite index column order rules. Covering indexes. Why an index can make a query SLOWER (over-indexing, low cardinality columns).

- **Transactions ****&**** ACID: **atomicity, consistency, isolation, durability — don't just define them, know how each is implemented (WAL for durability, MVCC for isolation in Postgres).

- **Isolation levels: **Read Uncommitted, Read Committed, Repeatable Read, Serializable. Dirty reads, non-repeatable reads, phantom reads — be able to construct an example transaction interleaving for each.

- **MVCC: **how Postgres avoids read locks using row versioning, what a vacuum does and why bloat happens.

- **Locking: **row-level vs table-level locks, deadlocks and how the DB detects/resolves them, optimistic vs pessimistic concurrency control.

- **Concurrency control trivia that comes up in interviews: **what happens when two transactions update the same row concurrently under each isolation level.

*Resource: “CMU Intro to Database Systems” (Andy Pavlo) — free, full lectures on YouTube, the gold standard for DB internals. Watch lectures 1–3, 6–9, 14–16 minimum. This single course will out-class 90% of DE candidates who only know SQL syntax.*

## 1.2 — Relational Algebra & SQL Theory

SQL syntax you already have. The theory underneath separates people who can write queries from people who can explain why a query is correct.

- Relational algebra operators: selection, projection, join (and the 4 join algorithms), union/intersect/difference, set operations — map every SQL clause back to its algebra operator

- Set theory underpinning SQL: NULL is not a value, three-valued logic (TRUE/FALSE/UNKNOWN), why NULL breaks naive equality checks

- Normalization theory properly: functional dependencies, 1NF–3NF (you have this), BCNF, and WHY denormalization is a deliberate engineering tradeoff in OLAP — not a mistake

- Query optimization theory: cost-based optimization, statistics/histograms the planner uses, predicate pushdown, join order optimization

- Window functions theory: frame specifications (ROWS vs RANGE), partition vs order — go beyond syntax to understand frame boundaries deeply since this is a top interview differentiator

## 1.3 — Data Modeling: The Gap You Flagged

This is explicitly one of your weak areas. Spend real time here — it's also one of the highest ROI topics because most candidates only know 3NF and freeze when asked to design a star schema.

### OLTP modeling (you have the basics)

- Entity-relationship modeling, cardinality, normalization to 3NF — review quickly, you know this

### OLAP / analytical modeling (your gap)

- **Kimball dimensional modeling: **fact tables vs dimension tables, grain definition (the single most important and most skipped step), star schema vs snowflake schema, and when to choose each

- **Fact table types: **transaction fact, periodic snapshot fact, accumulating snapshot fact — know a real business example of each

- **Slowly Changing Dimensions (SCD): **Type 0 through Type 6 — but really master Type 1 (overwrite), Type 2 (historical versioning with effective dates), and Type 3 (limited history). This comes up in almost every DE interview.

- **Conformed dimensions ****&**** the bus matrix: **how large orgs keep dimension definitions consistent across many fact tables

- **Inmon vs Kimball vs Data Vault: **the three major modeling philosophies — know the actual tradeoffs (Inmon = normalized enterprise warehouse first; Kimball = dimensional marts first; Data Vault = hub/link/satellite for auditability and agile change). Modern lakehouses often use a hybrid.

- **Data Vault 2.0 (at least conceptually): **hubs, links, satellites — increasingly relevant in regulated industries (finance, healthcare) for full historical traceability

- **One Big Table (OBT) / wide denormalized modeling: **the modern lakehouse-era counter-trend to star schemas, used when compute is cheap (Snowflake/BigQuery/Databricks) and joins are the bottleneck. Know WHEN this beats Kimball.

*Resource: “The Data Warehouse Toolkit” by Ralph Kimball — still the bible for dimensional modeling, 25+ years on. Read chapters 1–3 minimum. Pair with Joe Reis **&** Matt Housley**'**s “Fundamentals of Data Engineering” (O**'**Reilly) for the modern lakehouse-era view.*

## 1.4 — Advanced SQL Patterns (push past where you are now)

- Recursive CTEs and graph/hierarchy traversal — you've already done transitive closure, now do: org chart traversal, bill-of-materials explosion, shortest path in a graph stored as edges table

- Gaps and islands problems (classic interview pattern)

- Sessionization with window functions (time-gap based session assignment)

- Pivoting/unpivoting (CASE WHEN aggregation, and native PIVOT where supported)

- Deduplication patterns: ROW_NUMBER() OVER(PARTITION BY...) vs DISTINCT ON (Postgres-specific) — know tradeoffs

- Slowly changing data queries: “as of” point-in-time queries against Type 2 SCD tables

- Query performance debugging: reading actual EXPLAIN ANALYZE output and rewriting a slow query

*Resource: StrataScratch (you**'**re already using it — keep going), DataLemur for FAANG-style SQL interview questions, and “SQL Antipatterns” by Bill Karwin for what NOT to do.*

# Phase 2 — Python for Data Engineering, Done Properly

Weeks 6–9 · ~25 hrs/week · You already script in Python with OOP and SQLAlchemy. This phase makes your Python production-grade — the kind that survives code review at a real company, not just “it runs on my machine.”

## 2.1 — Python Internals That Matter for Data Work

- **Memory model: **how Python objects are stored, reference counting + garbage collection, why this matters for processing large datasets in memory

- **GIL (Global Interpreter Lock): **what it is, why CPU-bound multi-threading doesn't parallelize in Python, and why this pushes DE workloads toward multiprocessing or external engines (Spark) instead

- **Generators ****&**** iterators: **lazy evaluation for processing files/streams larger than memory — this is not optional for DE, it's core

- **Context managers: **writing your own with __enter__/__exit__ for resource handling (DB connections, file handles, S3 clients)

- **Decorators: **for retries, timing/logging, caching — you'll write a @retry decorator and a @timed decorator from scratch, not import one

## 2.2 — Concurrency & Parallelism (the part most self-taught DEs skip)

- threading vs multiprocessing vs asyncio — know exactly when to use each: I/O-bound (API calls, DB writes) → asyncio/threading; CPU-bound (transformation, parsing) → multiprocessing

- asyncio fundamentals: event loop, coroutines, awaitables — build one async pipeline that hits multiple APIs concurrently (you'll need this for API-heavy ingestion like your Jikan/anime pipeline, scaled up)

- ProcessPoolExecutor / concurrent.futures for CPU-bound parallel transforms

- Backpressure and rate limiting when calling external APIs at scale

## 2.3 — Writing Production-Grade Python (this is what AI tools can't shortcut for you)

- **Type hints everywhere: **mypy or pyright for static type checking — catches entire classes of bugs before runtime

- **Testing discipline: **pytest — unit tests, fixtures, mocking external services (S3, APIs, DBs) with moto/responses. Write tests for your Olist pipeline's transformation logic specifically.

- **Error handling philosophy: **fail-fast vs graceful degradation, custom exception hierarchies, structured logging (not print statements) with the logging module or structlog

- **Packaging: **proper project structure, pyproject.toml, virtual environments, building installable packages — not loose scripts

- **Code quality tooling: **black/ruff for formatting+linting, pre-commit hooks — set this up on your existing repos this week

- **Design patterns relevant to DE: **Factory pattern (you may already use this for connectors), Strategy pattern (swappable transformation logic), Singleton (connection pooling) — know WHY each pattern fits the problem, not just memorize them

## 2.4 — Data Processing Libraries, With Internals

- **pandas internals: **why it's single-threaded and memory-bound, vectorization vs apply() performance gap, dtype memory optimization, chunked reading for files larger than RAM

- **Polars: **the modern Rust-backed alternative — lazy evaluation, query optimization, multi-threading by default. Increasingly expected in 2026 job postings as a pandas-killer for medium data.

- **PyArrow: **the columnar in-memory format underneath Parquet, Polars, and increasingly pandas itself — understand Arrow as the modern interchange format between tools

- **SQLAlchemy (you know this) — push further: **Core vs ORM tradeoffs for ETL (Core is usually better for bulk loads), connection pooling tuning, bulk insert performance patterns (executemany vs COPY)

*Resource: “Fluent Python” by Luciano Ramalho for the internals (2nd edition covers async properly). “High Performance Python” by Gorelick **&** Ozsvald specifically for the performance/concurrency chapters.*

# Phase 3 — Distributed Systems Theory + Spark

Weeks 10–14 · ~30 hrs/week · You flagged this as a complete gap. This is also the section that most separates a junior DE from a mid-level one — it's where “can write a pipeline” becomes “can write a pipeline that doesn't fall over at 10x the data.”

## 3.1 — Distributed Systems Theory (the foundation, tool-agnostic)

Do NOT skip to Spark before this. Spark is an implementation of these ideas — if you don't know the ideas, you'll memorize Spark API calls without understanding why they exist.

- **CAP theorem: **Consistency, Availability, Partition tolerance — you can only have 2 of 3 during a network partition. Know real examples: Postgres (CP), Cassandra (AP).

- **Consistency models: **strong consistency, eventual consistency, causal consistency — and which analytical systems actually need which (hint: most batch DE doesn't need strong consistency, this is a key insight)

- **Partitioning / sharding strategies: **range partitioning, hash partitioning, consistent hashing — and the hot-partition problem

- **Replication: **leader-follower, multi-leader, leaderless — and the tradeoffs of each for durability vs latency

- **The MapReduce paradigm: **even though raw MapReduce is largely legacy, understanding map → shuffle → reduce is essential because Spark's execution model is a direct descendant of it

- **Distributed file systems: **HDFS concepts (blocks, replication, NameNode/DataNode) — even if you'll mostly use S3 in practice, knowing HDFS explains why S3-based lakes behave the way they do

- **Fault tolerance in distributed compute: **how a distributed job recovers from a worker node dying mid-task (lineage-based recovery, checkpointing)

*Resource: “Designing Data-Intensive Applications” by Martin Kleppmann — THE book. Chapters 1–6 are essential for any DE. This single book will carry you further in interviews than any tool tutorial. Free lecture series alternative: MIT 6.824 Distributed Systems (YouTube, free).*

## 3.2 — Apache Spark (PySpark)

Now the tool, with the theory already in place so each Spark concept clicks instead of being memorized.

- **Spark architecture: **Driver, Executors, Cluster Manager (YARN/Kubernetes/Standalone) — draw this from memory before touching code

- **RDDs vs DataFrames vs Datasets: **know RDDs exist and why DataFrames replaced them (Catalyst optimizer, Tungsten execution engine) — you'll mostly write DataFrame code but must understand what's underneath

- **Lazy evaluation ****&**** the DAG: **transformations vs actions, how Spark builds an execution plan before running anything

- **Catalyst optimizer ****&**** Tungsten: **how Spark optimizes your DataFrame code into an efficient physical plan — read .explain() output the way you read Postgres EXPLAIN ANALYZE

- **Partitioning in Spark: **default vs custom partitioning, repartition() vs coalesce(), the classic shuffle problem

- **Shuffles: **what triggers a shuffle (groupBy, join, repartition), why shuffles are expensive, and how to minimize them — this is THE top Spark performance topic in interviews

- **Joins in Spark: **broadcast join vs shuffle hash join vs sort-merge join, broadcast hints for small-table joins, and skew handling (salting technique for skewed join keys)

- **Caching/persistence: **MEMORY_ONLY vs MEMORY_AND_DISK, when caching helps vs hurts

- **Spark SQL: **writing SQL directly against DataFrames, and how it compiles to the same Catalyst plan as DataFrame API calls

- **Performance tuning: **executor memory/cores tuning, dynamic allocation, spotting and fixing data skew, avoiding small-file problems

- **PySpark specifically: **the JVM bridge (py4j) and why UDFs in pure Python are slow — prefer built-in functions or pandas UDFs (Arrow-vectorized) over Python UDFs

*Resource: “Learning Spark” 2nd edition (O**'**Reilly, free PDF from Databricks) + Databricks Academy free courses. Practice on Databricks Community Edition (free tier) so you get a real cluster, not just local mode.*

## 3.3 — Hands-on: Don't just read, rebuild

- Rebuild your Olist pipeline's heaviest transformation step in PySpark instead of pandas — compare performance and explain WHY the difference exists

- Deliberately create a data skew scenario and fix it with salting — you want to be able to talk through this in an interview from real experience, not theory

- Read 3–5 real .explain() plans from your own jobs and write a short note on what each stage is doing

# Phase 4 — Streaming Systems: Kafka + Real-Time Processing

Weeks 15–17 · ~25 hrs/week · Every pipeline you've built so far is batch. Real industry-grade DE roles increasingly expect at least working knowledge of streaming — this phase makes you conversant, not necessarily expert (that takes years on the job).

## 4.1 — Streaming Theory First

- **Batch vs streaming vs micro-batch: **the real tradeoffs — latency vs throughput vs complexity vs cost. Most companies don't need true streaming; know how to argue this in an interview.

- **Event time vs processing time: **the single most important streaming concept — late-arriving data, out-of-order events

- **Watermarks: **how streaming systems decide “we've waited long enough” for late data

- **Windowing: **tumbling, sliding, session windows — know a real use case for each

- **Exactly-once vs at-least-once vs at-most-once semantics: **what each guarantees, why exactly-once is hard in distributed systems, idempotency as the practical solution

## 4.2 — Apache Kafka

- **Core architecture: **topics, partitions, brokers, producers, consumers, consumer groups — draw this from memory

- **Partitioning strategy: **how keys map to partitions, why partition count affects parallelism and ordering guarantees

- **Replication ****&**** ISR (in-sync replicas): **how Kafka achieves durability and availability, leader election

- **Offsets ****&**** consumer groups: **how Kafka tracks consumption progress, rebalancing, and exactly the failure modes that cause duplicate or lost messages

- **Schema Registry: **Avro/Protobuf schema evolution — why you can't just dump JSON into Kafka in a serious production system

- **Kafka Connect: **source/sink connectors, the standard way to get data in/out of Kafka without custom code

- **Kafka Streams / ksqlDB: **lightweight stream processing directly on Kafka, vs full frameworks below

## 4.3 — Stream Processing Frameworks

- Spark Structured Streaming — since you're already learning Spark, this is your natural entry point: micro-batch model, watermarking API, integration with Kafka as a source

- Flink (awareness level) — true low-latency streaming, increasingly the industry standard for sub-second use cases. Know the conceptual difference from Spark Streaming (true streaming vs micro-batch) even if you don't go deep hands-on yet

- CDC (Change Data Capture) as the most common real-world streaming use case for a DE — covered in depth in Phase 7

*Resource: “Kafka: The Definitive Guide” (free from Confluent) for Kafka internals. Confluent**'**s free Kafka courses (developer.confluent.io) are excellent and hands-on. Run a local Kafka cluster via Docker Compose — don**'**t just read.*

## 4.4 — Build This

- A minimal real-time pipeline: a Python producer streaming events → Kafka → Spark Structured Streaming consumer → aggregation → Postgres sink. This single project, done end-to-end and explained well, signals more than most candidates' entire resume.

# Phase 5 — Cloud Depth: AWS Data Engineering, Properly

Weeks 18–21 · ~25 hrs/week · You know S3, Athena, Glue at a surface level. This phase goes deep on the AWS data stack specifically (your existing investment) plus enough breadth on GCP/Azure equivalents to be conversational — most job postings name a specific cloud, and AWS dominates DE postings in India.

## 5.1 — Storage Layer, Deeply

- **S3 internals: **consistency model (now strong read-after-write since 2020 — know this, it's a common stale-knowledge interview trap), storage classes and lifecycle policies, multipart uploads for large files, S3 as the foundation of every modern lakehouse

- **File formats deeply: **CSV/JSON (row-based, human readable, slow) vs Parquet (columnar, compressed, predicate pushdown, the industry standard) vs ORC vs Avro (row-based, schema evolution, good for streaming/Kafka). Know WHEN to use each — this is asked constantly.

- **Compression codecs: **Snappy vs Gzip vs Zstd — speed vs compression ratio tradeoffs

- **Partitioning strategy on S3: **Hive-style partitioning (year=2026/month=06/), partition pruning, the small-files problem and how to fix it (compaction)

## 5.2 — Query & Compute Layer

- **Athena deeply (you have surface level): **how it's Presto/Trino under the hood, cost model (pay per TB scanned — directly tie this back to partitioning and columnar format choices you just learned), CTAS for materializing transformed data

- **Glue deeply: **Glue Data Catalog as a Hive Metastore-compatible metadata layer, Glue Crawlers (and their real-world quirks/limitations), Glue ETL jobs (Spark-based managed compute) vs Glue Python Shell jobs

- **EMR: **managed Hadoop/Spark clusters — when to use EMR vs Glue vs Athena (cost and control tradeoffs)

- **Redshift: **MPP (massively parallel processing) architecture, distribution styles (KEY/ALL/EVEN), sort keys, when a real data warehouse beats a query-on-S3 approach

- **Lambda for DE: **event-driven micro-ETL, S3 trigger → Lambda pattern, and its limits (15 min timeout, memory ceiling) that push you toward Glue/EMR for heavier jobs

## 5.3 — IAM, Networking, Security (the part candidates skip and fail interviews on)

- IAM roles vs users vs policies — least-privilege design for a pipeline service role

- VPC basics: public/private subnets, security groups, why your Glue jobs need VPC endpoints to reach S3 privately

- Secrets management: Secrets Manager / Parameter Store — never hardcoded credentials, ever

- Cost awareness as an engineering skill: tagging resources, Athena scan costs, S3 storage tiering — increasingly interviewers ask “how would you reduce this pipeline's cost”

## 5.4 — Infrastructure as Code

- **Terraform: **the industry standard — learn to provision your own S3/Glue/IAM setup as code instead of clicking in the console. This is now a baseline expectation, not a nice-to-have, for DE roles in 2026.

- AWS CDK as an alternative (Python-native, useful since you're Python-strong) — know it exists, Terraform is still more universally expected

## 5.5 — Multi-cloud literacy (breadth, not depth)

You won't master 3 clouds. But know the AWS → GCP → Azure equivalents so you're not lost in an interview or job posting that uses different vendor names for the same concept:

| **Concept** | **AWS** | **GCP** | **Azure** |
| --- | --- | --- | --- |
| Object storage | S3 | Cloud Storage | Blob Storage |
| Managed warehouse | Redshift | BigQuery | Synapse Analytics |
| Serverless query-on-lake | Athena | BigQuery (native) | Synapse Serverless |
| Managed Spark | EMR / Glue | Dataproc | HDInsight / Synapse Spark |
| Orchestration | MWAA (managed Airflow) | Cloud Composer | Data Factory |
| Streaming | Kinesis | Pub/Sub + Dataflow | Event Hubs |

# Phase 6 — Orchestration, Data Quality, Observability

Weeks 22–24 · ~25 hrs/week · You know Kestra well already. This phase broadens you to the industry-default orchestrator (Airflow — still the most-requested in job postings even as Kestra/Dagster gain ground) and adds the data quality/observability layer most self-taught pipelines completely skip.

## 6.1 — Orchestration Theory (tool-agnostic)

- **DAGs as a concept: **why workflows must be acyclic, task dependencies, idempotency as a hard requirement for any production task (re-running a task must not double-count or corrupt data)

- **Backfilling: **running a pipeline for historical dates correctly — a very common interview and real-world scenario

- **Sensors / triggers vs scheduling: **event-driven vs time-based orchestration, and the tradeoffs

- **Retry ****&**** failure strategy design: **exponential backoff, dead-letter patterns, partial-failure handling in a multi-task DAG

## 6.2 — Apache Airflow

You know Kestra (YAML-based, modern). Airflow (Python-based, the incumbent) is still the single most-requested orchestrator in job postings — learn it specifically to be hireable, and to compare design philosophies.

- Core architecture: Scheduler, Webserver, Executor (Local/Celery/Kubernetes), Metadata DB

- DAG authoring in Python: operators, sensors, hooks, XComs for inter-task data passing

- TaskFlow API (modern Airflow 2.x+ style) vs classic operator style

- Airflow vs Kestra vs Dagster — be ready to articulate this comparison in an interview: Airflow = mature ecosystem, Python-native, more boilerplate; Kestra = YAML-declarative, lower barrier, newer; Dagster = asset-based (data-aware) orchestration, strong typing, increasingly favored for data quality-first teams

*Resource: Astronomer**'**s free Airflow guides (astronomer.io/guides) are the best practical reference. Run Airflow locally via Docker Compose (official astronomer/airflow quickstart) — don**'**t just read docs.*

## 6.3 — Data Quality & Testing (the layer most self-taught DEs never build)

- **Great Expectations: **declarative data quality assertions — schema checks, null checks, range checks, distribution checks — integrated into a pipeline so bad data fails loudly instead of silently corrupting downstream tables

- **dbt tests (you have dbt basics already): **built-in tests (unique, not_null, relationships, accepted_values) plus custom SQL-based tests — push deeper into this since you already have the dbt foundation

- **Data contracts: **the emerging practice of formal schema agreements between data producers and consumers — increasingly discussed in 2025–2026 DE job postings as orgs mature past “pipelines just break silently”

- **Testing strategy for pipelines: **unit tests for transformation logic, integration tests for the full pipeline against a test database, data quality tests for the actual output

## 6.4 — Observability (how you know it's broken before your boss does)

- Structured logging across a pipeline — correlation IDs to trace a single record's journey through multiple stages

- Metrics: row counts in/out per stage, processing duration, freshness (data lag) — the bare minimum every production pipeline needs

- Alerting design: when to alert (and the discipline of avoiding alert fatigue) — you already do Slack alerting in your taxi-reporter and weather pipelines, now formalize the PATTERN: what conditions warrant a page vs a log line

- dbt artifacts + dbt docs for pipeline lineage visibility — generate and read a lineage graph

- OpenLineage / data lineage concept — increasingly expected awareness even if you don't deploy a full lineage platform (Marquez, DataHub) yourself

# Phase 7 — Modern Lakehouse Stack: dbt, Iceberg/Delta, CDC

Weeks 25–26 · ~25 hrs/week · This is the “beat the competition” phase — these are the tools and concepts that show up in job postings from companies actually building modern data platforms in 2026, and that most bootcamp-trained candidates have never touched.

## 7.1 — dbt, Properly (push past basics)

- Project structure: staging → intermediate → marts layering convention

- Jinja templating + macros for DRY SQL

- Incremental models: the is_incremental() pattern, merge vs append vs delete+insert strategies — directly relevant to your Olist pipeline's PostgreSQL incremental upsert work

- Snapshots for SCD Type 2 — dbt automates exactly the slowly changing dimension pattern from Phase 1, implement it for real

- Packages (dbt_utils, dbt_expectations) and when to reach for them vs write custom

- dbt semantic layer / MetricFlow (newer dbt feature) — centralized metric definitions, increasingly a differentiator to know

## 7.2 — Table Formats: The Single Biggest Shift in Modern Data Engineering

This is the area where being current matters most — these formats didn't widely exist 5 years ago and now define what “modern lakehouse” means. Knowing this well is a genuine competitive edge over candidates stuck on “dump files in S3.”

- **The problem they solve: **raw Parquet-on-S3 has no ACID guarantees, no schema evolution safety, no time travel, and the small-files problem — table formats add a transaction/metadata layer on top

- **Apache Iceberg: **the increasingly dominant open table format — hidden partitioning, schema evolution without rewriting data, time travel queries, snapshot isolation. AWS Glue/Athena, Snowflake, and Databricks all now support it natively.

- **Delta Lake: **Databricks' table format — transaction log (_delta_log), ACID on top of Parquet, similar goals to Iceberg via a different design. Know the conceptual overlap and the main practical difference: Delta is most native inside Databricks; Iceberg has broader multi-engine adoption.

- **Apache Hudi: **the third major format, strongest historically for upsert-heavy/CDC-heavy workloads — know it exists and its niche, lower priority for hands-on depth than Iceberg

- **Hands-on: **build a small pipeline writing to Iceberg tables via Athena or a local Spark+Iceberg setup, perform a schema evolution and a time-travel query, and be able to explain what's happening in the metadata layer

## 7.3 — Change Data Capture (CDC) — the most common real streaming use case

- **What CDC solves: **capturing row-level inserts/updates/deletes from an OLTP database (like your Postgres) and propagating them downstream without batch re-extraction of the whole table

- **Log-based CDC: **reading the database's write-ahead log (Postgres WAL, MySQL binlog) directly — the modern, low-impact approach vs old trigger-based or query-based CDC

- **Debezium: **the open-source standard for log-based CDC, runs as a Kafka Connect source connector — ties directly back to your Phase 4 Kafka knowledge

- **Hands-on: **set up Debezium against your local Postgres, capture changes into Kafka, and land them in S3 as Iceberg/Delta upserts. This single project — Postgres → Debezium → Kafka → Spark Streaming → Iceberg — demonstrates the full modern real-time lakehouse stack and is a genuine standout portfolio piece for a junior candidate.

## 7.4 — The Modern Data Stack, Named and Mapped

Know what each category does and 1–2 real tools in it — this vocabulary alone signals currency in interviews:

| **Layer** | **Purpose** | **Examples** |
| --- | --- | --- |
| Ingestion (EL) | Move raw data from source to lake/warehouse | Airbyte, Fivetran, custom Python |
| Storage | Durable, cheap, scalable raw + processed storage | S3, GCS, ADLS |
| Table format | ACID + schema evolution + time travel on object storage | Iceberg, Delta Lake, Hudi |
| Transformation (T) | Turn raw data into modeled, tested, documented tables | dbt, SQLMesh |
| Orchestration | Schedule, sequence, retry pipeline tasks | Airflow, Kestra, Dagster |
| Compute engine | Run heavy transforms/queries | Spark, Trino/Athena, Snowflake, BigQuery |
| Streaming | Real-time data movement and processing | Kafka, Flink, Debezium |
| Quality/Observability | Catch bad data and broken pipelines fast | Great Expectations, Monte Carlo, dbt tests |
| Catalog/Governance | Discoverability, lineage, access control | DataHub, Glue Catalog, Unity Catalog |

# Phase 8 — System Design for Data Engineers

Ongoing from Week 10 onward, intensive in Weeks 22–26 · You flagged this as a gap and it's arguably the single highest-stakes interview round for anyone beyond pure-junior level. DE system design is different from backend system design — it's about data flow, volume, and consistency, not request/response latency.

## 8.1 — The DE System Design Framework

Use this structure every time, in interviews and practice — interviewers are grading your PROCESS, not just your final diagram:

- Clarify requirements: data volume, velocity, variety; batch or real-time; SLA for freshness; who consumes it and how

- Estimate scale: back-of-envelope math — rows/day, GB/day, peak throughput. Always show this math out loud.

- Choose the high-level architecture: ingestion → storage → processing → serving, naming a real tool at each stage with a stated reason

- Go deep on 1–2 components the interviewer probes — usually the trickiest part (dedup, late data, schema evolution, exactly-once)

- Discuss failure modes and tradeoffs explicitly: what breaks, how you'd detect it, how you'd recover

- Discuss cost and operational complexity — senior interviewers specifically listen for this; juniors who only talk about “what works” stand out as junior

## 8.2 — Classic DE System Design Problems to Practice

- Design a pipeline to ingest clickstream events from a website at 100K events/sec

- Design a data warehouse for an e-commerce company (directly maps to your Olist project — you can use real experience here)

- Design a real-time fraud detection data pipeline

- Design a CDC pipeline to sync a production OLTP database to an analytical warehouse with under 5 minutes of lag

- Design a system to deduplicate and reconcile data from 5 different upstream sources with inconsistent schemas

- Design a metrics/analytics platform serving dashboards for 1000s of internal users with sub-second query latency

- Design a slowly-changing-dimension-aware customer 360 table

## 8.3 — Core Tradeoffs You Must Be Fluent In

| **Tradeoff** | **When to lean which way** |
| --- | --- |
| Batch vs Streaming | Batch: simpler, cheaper, fine for most reporting. Streaming: only when sub-minute freshness has real business value (fraud, ops alerting). |
| Normalize vs Denormalize | Normalize for OLTP/write-heavy. Denormalize (star schema or OBT) for OLAP/read-heavy analytics. |
| ELT vs ETL | ELT (modern default): push raw data in, transform with warehouse compute (dbt). ETL: still used when source systems are sensitive/regulated or compute is genuinely the bottleneck. |
| Push vs Pull | Push (event-driven/CDC) for freshness. Pull (scheduled batch) for simplicity and predictable cost. |
| Schema-on-write vs schema-on-read | Schema-on-write (warehouse) for governed, query-optimized data. Schema-on-read (lake) for flexibility with raw/varied data. |
| Build vs Buy | Build when it's core differentiation or no managed tool fits. Buy (Fivetran/Airbyte) for commodity ingestion — most companies shouldn't hand-write every connector. |

*Resource: “The System Design Interview” by Alex Xu has a data-pipeline-adjacent chapters; but for DE-specific system design, the strongest free resource is working through real engineering blog posts from Uber, Airbnb, Netflix, and Doordash**'**s data platform teams — search their engineering blogs for “data pipeline,” “real-time architecture,” “data platform.” These are literally the systems interviewers model their questions on.*

# Phase 9 — The AI-Proofing Layer: What Actually Beats Competition

This is the section that answers your actual question directly: what makes you NOT replaceable, and what beats other candidates (human or AI-assisted).

## 9.1 — Why “AI-proof” is the wrong frame, and the right one

AI tools (including Claude) are extremely good at writing a DAG, a transformation script, or boilerplate dbt models when given a clear spec. They are weak at:

- Knowing WHAT to build when requirements are vague, political, or contradictory (real business stakeholders rarely give clean specs)

- Diagnosing WHY a production pipeline that 'should work' is silently producing wrong numbers — this requires understanding the full stack from DB internals to distributed execution, exactly what Phases 1–3 build

- Making cost/tradeoff judgment calls with organizational context an AI doesn't have

- Being trusted with production access, on-call responsibility, and accountability — a structural/trust gap, not a knowledge gap

The real skill that makes you valuable isn't “write code AI can't write” — it's “be the person who can specify, verify, debug, and take responsibility for what AI-assisted tooling produces.” That's an engineer who deeply understands the system, which is exactly what this entire roadmap builds.

## 9.2 — Concrete Differentiators (do these, most candidates don't)

- **1. Use AI tools AS a force multiplier, visibly: **in your portfolio README and interviews, be open that you use Claude/Copilot for boilerplate — but show you reviewed, tested, and understood every line. Hiring managers in 2026 don't want people who refuse AI tools; they want people who use them without losing engineering judgment.

- **2. Write real postmortems: **when something breaks in your own pipelines (it will), write a short postmortem — root cause, impact, fix, prevention. Put 2–3 of these in your portfolio repo. Almost no junior candidate has this; it directly signals production maturity.

- **3. Cost-optimize a real pipeline and document it: **take your Olist Athena pipeline, measure the bytes-scanned cost before and after a partitioning/format change, write up the before/after with numbers. This single artifact is more convincing than 10 more tutorial projects.

- **4. Contribute to one open-source DE tool: **even a small docs fix or bug fix to dbt, Kestra, Airflow, or Polars. This is disproportionately rare among junior candidates and disproportionately respected by senior interviewers.

- **5. Go deep on ONE end-to-end modern project, not five shallow ones: **your Postgres → Debezium → Kafka → Spark Streaming → Iceberg pipeline (Phase 7) IS that project. One pipeline that demonstrates CDC + streaming + lakehouse table format + orchestration + data quality + observability beats five separate “I moved data from A to B” projects.

- **6. Be able to whiteboard, not just code: **practice explaining your Olist pipeline's architecture out loud, from memory, with a diagram, in under 3 minutes. This single skill is what your own SQL assessment flagged as a remaining gap — verbal explanation under observation. Practice it deliberately, not just the technical content.

- **7. Know the business, not just the data: **for every project, be able to state in one sentence WHY a business would pay for this pipeline to exist. Interviewers notice candidates who think about data as a tool for decisions, not just an engineering exercise.

## 9.3 — Staying Current (the ongoing, never-finished part)

- Follow 3–5 DE-focused newsletters/blogs: Data Engineering Weekly, Seattle Data Guy (YouTube), Andreessen Horowitz's data infrastructure posts, the engineering blogs of Netflix/Uber/Airbnb data platform teams

- Re-visit the 'Modern Data Stack' table (Phase 7.4) every quarter — this space moves fast and new entrants (e.g., new query engines, new orchestration tools) appear regularly

- Follow the State of Data Engineering survey results (published annually) to know what's actually being adopted in industry, not just hyped

# Daily Non-Negotiables — SQL + DSA Practice System

This runs EVERY single day of the 6 months, regardless of which phase you're in. This is what builds interview confidence — not cramming the week before an interview, but having solved 500+ SQL problems and 150+ DSA problems by Month 6 through pure consistency.

*Rule: this comes BEFORE phase study time, not after. If you only have energy for one thing today, this is the one thing. 45–75 minutes total, every day, no exceptions — treat it like brushing your teeth, not like a study session you can skip when busy.*

## The Daily Block (~60–75 min)

| **Block** | **Time** | **What** |
| --- | --- | --- |
| 3 SQL problems | 30–40 min | 1 easy (warm-up/speed), 1 medium (pattern practice), 1 hard (window fns, recursive CTEs, multi-step logic) |
| 1 DSA problem (Python) | 25–35 min | Rotate through topics weekly (see schedule below). Write, run, and verbalize the approach out loud before coding. |
| Review | 5 min | Add any new pattern to your Anki deck or a running 'patterns.md' file in your lab repo |

## SQL Rotation — Where to Pull Problems

- StrataScratch (you already use this) — best for real company-style business questions

- DataLemur — best for FAANG-style SQL interview questions specifically, free tier is generous

- LeetCode Database section — good for timed practice under interview-like constraints

- Your OWN data: once a week, write a new analytical query against your Olist or taxi dataset instead of a practice site — real messy data teaches things clean practice problems don't

## SQL Topic Coverage Checklist (cycle through all of these across the 6 months)

| **Category** | **Patterns to drill** |
| --- | --- |
| Joins | Inner/left/right/full, self-joins, anti-joins (NOT EXISTS), multi-table joins |
| Aggregation | GROUP BY with HAVING, multi-level aggregation, conditional aggregation (CASE inside SUM/COUNT) |
| Window functions | ROW_NUMBER, RANK, DENSE_RANK, LAG/LEAD, running totals, moving averages, frame clauses |
| CTEs | Multi-step CTEs, recursive CTEs (hierarchies, graphs) |
| Subqueries | Correlated vs uncorrelated, subqueries in SELECT/WHERE/FROM |
| String/date functions | Regex matching, date truncation/bucketing, string parsing |
| Set operations | UNION/UNION ALL/INTERSECT/EXCEPT, when each applies |
| Classic patterns | Gaps and islands, sessionization, dedup, pivot/unpivot, top-N-per-group |
| Performance | Reading EXPLAIN ANALYZE, identifying missing indexes, rewriting a slow query |

## DSA Weekly Rotation (Python)

Goal by Month 6: 150+ problems solved, comfortable explaining time/space complexity out loud, can solve most Medium LeetCode problems in under 25 minutes. This is NOT about becoming a competitive programmer — DE interviews rarely go beyond Medium difficulty, but you must be FAST and CONFIDENT, which only comes from volume.

| **Week** | **Focus topic** | **Why it matters for DE** |
| --- | --- | --- |
| 1–2 | Arrays & Strings | Foundation — most data manipulation logic reduces to this |
| 3–4 | Hash Maps & Sets | THE most common DE-adjacent pattern — dedup, grouping, frequency counting mirror real pipeline logic |
| 5–6 | Two Pointers & Sliding Window | Stream processing intuition — windowing concepts from Phase 4 connect directly here |
| 7–8 | Recursion & Backtracking | Builds the muscle for recursive CTEs and tree/graph traversal |
| 9–10 | Trees & Graphs (BFS/DFS) | Directly maps to DAG traversal (orchestration), hierarchy queries (recursive SQL), lineage graphs |
| 11–12 | Sorting & Searching | Binary search patterns, understanding sort complexity ties to query optimizer behavior |
| 13–14 | Linked Lists & Stacks/Queues | Common interview warm-up topics, also underlie streaming buffer/queue concepts |
| 15–16 | Dynamic Programming (light) | Lower priority for DE — cover the basics (fibonacci-style, simple knapsack) but don't over-invest; DE interviews rarely go deep DP |
| 17–18 | Heaps & Priority Queues | Top-K problems — directly relevant to 'top N per group' SQL patterns and stream processing |
| 19–26 | Mixed review + timed mock rounds | Re-cycle weak topics, simulate real 25–45 min interview timing |

- Primary platform: LeetCode (free tier covers everything you need)

- Secondary: NeetCode 150 list (free, curated, exactly the right scope for DE-adjacent interviews — don't grind random problems, follow this curated list)

## Weekly Mock Interview (start Month 3 onward)

- Once a week: do 1 SQL problem and 1 DSA problem completely out loud, narrating your thinking, on a timer — record yourself or practice with a peer. This is what closes your self-identified gap: live performance under observation.

- Use Pramp or peer-to-peer practice (find IITM/DE Zoomcamp community peers) for real mock interviews starting Month 4

# Capstone Projects — Portfolio That Gets Interviews

You already have 4 solid projects (taxi-slack-reporter, weather ETL, anime pipeline, Olist). Don't abandon them — finish Olist, then add these 3 capstones that specifically demonstrate the gaps you flagged. Each one should have a proper README with architecture diagram, design decisions explained, and a short 'what I'd do differently at 10x scale' section — that last part is what makes a portfolio project read as senior thinking.

### Capstone 1: Finish Olist (Months 1–2, alongside Phase 1–2)

- Complete the PostgreSQL incremental upsert layer and Kestra orchestration you have remaining

- Add: a proper dimensional model on top (you'll have just learned Kimball modeling — apply it here for real, define fact/dim tables and grain explicitly)

- Add: dbt tests + a few Great Expectations checks once you reach Phase 6

- Add: a cost analysis of the Athena layer (bytes scanned before/after partitioning) — this is the 'cost-optimize and document' differentiator from Phase 9

### Capstone 2: Distributed Batch Reprocessing Engine (Month 4, Phase 3)

Take your largest existing dataset (Olist or a new large public dataset) and build a PySpark pipeline that:

- Reads raw data from S3/MinIO, performs a non-trivial transformation (multi-table join + aggregation at scale)

- Deliberately handles a skewed join key with the salting technique — document the before/after performance

- Writes output partitioned and in Parquet, with a written explanation of the partitioning choice

- Includes a written note: 'this ran fine on pandas at X rows, here's where pandas would have broken, here's why Spark doesn't'

### Capstone 3: The Modern Lakehouse CDC Pipeline (Months 5–6, Phase 4 + 7)

This is your flagship project — the one you lead with in interviews. It single-handedly demonstrates streaming, CDC, table formats, and orchestration:

- Postgres (OLTP source, simulate an e-commerce orders table with ongoing inserts/updates)

- → Debezium (log-based CDC, captures inserts/updates/deletes)

- → Kafka (event backbone)

- → Spark Structured Streaming (consumes, applies watermarking for late events)

- → Apache Iceberg table on S3/MinIO (upserts via merge, with a demonstrated schema evolution and a time-travel query)

- → Orchestrated health checks and alerting via Kestra or Airflow

- Written architecture doc explaining exactly-once handling, late-data strategy, and what you'd change for 100x the event volume

### Capstone 4: System Design Writeups (ongoing, Months 4–6)

- Pick 4–5 of the classic problems from Phase 8.2 and write a full design doc for each — requirements, scale estimation, architecture diagram, tradeoffs, failure modes. Put these in your repo as markdown. This becomes your interview prep AND a portfolio artifact — very few junior candidates have written system design docs proactively.

# Interview Preparation System

Your own SQL assessment already identified two specific gaps: live performance under observation, and verbal explanation of design choices. Both are addressed by deliberate practice, not more study — you already know enough SQL, the gap is performance under pressure.

## The 4 Interview Rounds You'll Face (typical DE loop)

| **Round** | **What it tests** | **How this roadmap prepares you** |
| --- | --- | --- |
| SQL screen | Speed + correctness under time pressure | Daily 3 SQL problems, weekly timed mocks from Month 3 |
| Coding/DSA round | Python fundamentals, problem-solving communication | Daily 1 DSA problem, NeetCode 150, weekly verbalized mocks |
| System design | Architecture thinking, tradeoff reasoning | Phase 8 framework + Capstone 4 written design docs |
| Behavioral / project deep-dive | Can you explain YOUR work clearly, own decisions, discuss failures | Capstone projects with documented design decisions + postmortems |

## Project Deep-Dive Prep (this is where most candidates lose points)

For EVERY project in your portfolio, prepare crisp answers to:

- Why did you build this? (business framing, not just 'to learn X')

- Walk me through the architecture in under 2 minutes, ideally with a diagram you can draw from memory

- What was the hardest technical problem, and how did you solve it?

- What would break first if this had to handle 100x the data?

- What would you do differently if you rebuilt it today?

- What's a mistake you made on this project and what did it teach you?

## Practice Cadence

| **Month** | **Interview prep focus** |
| --- | --- |
| 1–2 | Daily SQL+DSA only. No mocks yet — building the base. |
| 3 | Start weekly self-recorded mock: 1 SQL + 1 DSA, narrated out loud, timed |
| 4 | Add system design practice — 1 design doc per week from the classic problems list |
| 5 | Start peer/Pramp mock interviews — full loop simulation (SQL + DSA + 1 system design) |
| 6 | Full mock loops weekly, refine project deep-dive answers, apply actively |

# Full Resource Library

Consolidated list of every resource mentioned, organized by type, plus a few extras. All free or low-cost — deliberately, given your situation.

## Courses (free)

- CMU Intro to Database Systems (Andy Pavlo) — YouTube, full DB internals course

- MIT 6.824 Distributed Systems — YouTube, the standard distributed systems course

- DE Zoomcamp (DataTalksClub) — you've already used parts of this, it covers the full modern stack end-to-end

- Databricks Academy (free tier courses) — Spark specifically

- Confluent Developer (developer.confluent.io) — free Kafka courses, excellent and hands-on

- Astronomer Airflow Guides (astronomer.io/guides) — best practical Airflow reference

## Books

- “Designing Data-Intensive Applications” — Martin Kleppmann (THE book, read chapters 1–6 minimum)

- “The Data Warehouse Toolkit” — Ralph Kimball (dimensional modeling bible)

- “Fundamentals of Data Engineering” — Joe Reis & Matt Housley (modern lakehouse-era overview)

- “Fluent Python” — Luciano Ramalho (Python internals + async)

- “High Performance Python” — Gorelick & Ozsvald (concurrency/performance)

- “Learning Spark” 2nd ed. — free PDF from Databricks

- “Kafka: The Definitive Guide” — free from Confluent

- “SQL Antipatterns” — Bill Karwin

## Practice Platforms

- StrataScratch, DataLemur — SQL interview practice

- LeetCode (Database section + NeetCode 150 list) — SQL + DSA

- Databricks Community Edition (free) — real Spark cluster practice

- Pramp — free peer mock interviews

## Tools to Install/Set Up This Month

- Terraform — IaC for your AWS lab

- Docker Compose stack: Postgres + MinIO + Kafka + Kestra/Airflow locally

- Great Expectations + dbt (extend what you have)

- Debezium (via Docker) for CDC practice

- Spark + Iceberg local setup (or via Databricks Community Edition)

- ruff/black + mypy + pytest + pre-commit — set up on ALL existing repos this month, not just new ones

## Stay-Current Sources

- Data Engineering Weekly (newsletter)

- Seattle Data Guy (YouTube)

- Engineering blogs: Netflix, Uber, Airbnb, Doordash data platform teams

- Annual “State of Data Engineering” survey reports

# 6-Month Week-by-Week Tracker

Print or copy this into your own tracker. Daily SQL+DSA practice runs underneath EVERY week regardless of phase — not repeated in each row below, but never skipped.

| **Week** | **Phase / Focus** | **Key deliverable** |
| --- | --- | --- |
| 0 | Foundations Audit | Skill inventory done, lab repo + Docker stack set up |
| 1–2 | DB internals (storage, indexing, transactions) | Can explain MVCC, isolation levels, B-Tree vs LSM from memory |
| 3 | Relational algebra & SQL theory | Map every SQL clause to its algebra operator |
| 4–5 | Data modeling (Kimball, SCD, Data Vault) + advanced SQL patterns | Olist gets a real dimensional model with defined grain |
| 6–7 | Python internals + concurrency | Async pipeline hitting multiple APIs built |
| 8–9 | Production-grade Python + Polars/PyArrow | Tests, types, linting on ALL existing repos |
| 10–11 | Distributed systems theory (CAP, partitioning, replication) | Can draw MapReduce + fault tolerance from memory |
| 12–14 | Spark / PySpark deep dive | Capstone 2 (skewed join, salting) built and documented |
| 15–16 | Streaming theory + Kafka | Local Kafka cluster running, core architecture understood |
| 17 | Spark Structured Streaming + Flink awareness | Producer → Kafka → Spark → Postgres mini pipeline built |
| 18–19 | AWS storage + compute layer deep dive | Athena cost analysis on Olist documented |
| 20 | IAM/networking/security + Terraform | Olist AWS infra provisioned via Terraform |
| 21 | Multi-cloud literacy | Can map AWS→GCP→Azure equivalents from memory |
| 22 | Airflow + orchestration theory | Local Airflow running, 1 DAG migrated from Kestra as exercise |
| 23 | Data quality (Great Expectations, dbt tests) | Quality checks added to Olist pipeline |
| 24 | Observability | Metrics + alerting formalized across all existing pipelines |
| 25 | dbt deep dive + table formats (Iceberg/Delta) | Schema evolution + time travel demo built |
| 26 | CDC with Debezium | Capstone 3 flagship pipeline complete + documented |
| Ongoing 10–26 | System design practice | 5+ design docs written (Capstone 4) |
| Month 4–6 | Mock interviews + active applications | Weekly mocks, applying to roles from Month 4 onward |

## A Note on Pacing

This is an ambitious but realistic plan at 4–6 hrs/day. If a phase runs long, let it — the theory phases (1 and 3) are worth protecting even if it pushes the timeline to 7 months. Going deep on fewer things beats rushing through everything shallowly. That's also, not coincidentally, the entire thesis of this roadmap: depth is what AI tools can't shortcut for you, and depth is what gets you hired.

Start applying for internships/roles from Month 4 onward, not Month 6 — you'll be ready earlier than this document implies for many roles, and interview experience itself is part of the learning loop. Don't wait for 'complete' to start applying.

Page  of