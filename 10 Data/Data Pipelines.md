---
tags: [data, pipelines, data-engineering]
phase: 4
---
# 🚰 Data Pipelines & Data Engineering (for backend engineers)

## Concepts
- [ ] OLTP vs OLAP; row vs columnar storage
- [ ] ETL vs ELT; batch vs streaming; lambda vs kappa architecture
- [ ] **CDC (Change Data Capture)** with Debezium ⭐
- [ ] Data lake, warehouse, **lakehouse** (Apache Iceberg / Delta Lake table formats), Parquet
- [ ] Orchestration: **Airflow** / Dagster (DAGs, retries, backfills)
- [ ] Stream processing: **Apache Flink** / Kafka Streams / Spark Structured Streaming: windows, watermarks, late data, state
- [ ] Batch processing: Spark basics (awareness)
- [ ] Data quality, schema evolution, lineage, idempotent pipelines, backfills
- [ ] Transformations with **dbt** (awareness)
- [ ] OLAP stores: **ClickHouse**, BigQuery, Snowflake, Druid/Pinot (real-time analytics)
- [ ] Pipelines for AI: document ingestion → chunk → embed → index ([[RAG]])

## 🧪 Labs (🟢 warm-up → 🟡 core → 🔴 hard → ⚫ boss)
- [ ] 🟡 Ingestion pipeline: S3 → parse → chunk → embed → pgvector; idempotent + resumable
- [ ] 🔴 CDC → Kafka → ClickHouse with materialized views for cost per tenant
- [ ] 🔴 A Flink SQL or Kafka Streams windowed aggregation with late events
- [ ] ⚫ A backfill: re-embed 100k chunks with a new model with zero downtime (versioned index + alias swap)

## 🧠 Cognitive tasks
- [ ] Fermi: embedding cost + time for 1M docs; verify on 10k

## 🛰️ Orbit integration
- [ ] orbit-knowledge ingestion + orbit-analytics

> [!info] Go deeper
> 🧩 [[Distributed & Cloud Patterns]] (pipes & filters, claim check)

## Resources
- *Fundamentals of Data Engineering* (Reis & Housley) ⭐ · *Streaming Systems* (Akidau et al.)
- DataTalksClub **Data Engineering Zoomcamp** (free) ⭐ · Debezium tutorial · ClickHouse docs
