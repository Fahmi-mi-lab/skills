# Storage & Lineage

## What this covers
Where data physically lives at each stage, and how to trace a piece of data back to its origin (lineage) — critical for debugging, auditing, and trust in the platform.

## Storage architecture
- **Storage technology per layer** — e.g. object storage (S3/GCS/ADLS) for bronze/silver in a lakehouse, a data warehouse (BigQuery, Snowflake, Redshift) for gold, or a single lakehouse format (Delta Lake, Iceberg, Hudi) spanning all layers.
- **File format** — Parquet, ORC, Avro, Delta/Iceberg table format — note the choice and why (columnar formats are standard for analytical workloads).
- **Partitioning strategy** — how data is physically partitioned (commonly by date) to keep queries efficient and avoid scanning unnecessary data.
- **Retention policy** — how long data is kept at each layer (raw data often kept longer for reprocessing/compliance than curated data).

## Data lineage
Lineage answers: "where did this piece of data come from, and what transformations touched it along the way?"
- **Table-level lineage** — which source tables/datasets feed into which downstream tables.
- **Column-level lineage** (more advanced) — which source columns specifically feed into which target columns, useful when debugging a specific metric.
- Lineage should be traceable end-to-end: source → bronze → silver → gold → consumption (dashboard/ML feature/report).

## Representation in Penpot
Frame `04-Storage-Lineage`: can be split into two halves or two frames — (a) a storage architecture diagram showing which storage technology backs each layer, and (b) a lineage diagram showing arrows from source datasets through each transformation stage to final consumption points. Use a consistent arrow style for lineage that's distinct from the pipeline DAG's task-dependency arrows (lineage tracks *data*, not *task execution order*, so keep the two visually distinguishable even though they often look similar).

## Polish checklist
- [ ] Storage technology and file format are specified per layer, not left generic
- [ ] Partitioning strategy is stated for large/frequently-queried tables
- [ ] Retention policy differences between layers are noted
- [ ] Lineage arrows are traceable end-to-end from source to consumption without gaps
