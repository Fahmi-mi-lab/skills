# Source & Ingestion

## What this covers
Every data platform starts with knowing exactly where data comes from and how it gets in. Get this wrong and every downstream layer inherits the wrong assumptions about freshness, volume, and format.

## Source inventory
For every data source, capture:
- **Source name & type** — e.g. production Postgres DB, third-party API, IoT sensor stream, mobile app event log, CSV drop from a partner.
- **Format** — structured (tables), semi-structured (JSON, Avro), unstructured (logs, images).
- **Volume & growth rate** — current size, expected growth.
- **Update pattern** — how often the source changes (append-only, updates, deletes).
- **Access method** — direct DB connection, API, file drop (SFTP/S3), CDC (Change Data Capture), message queue/event stream.
- **Owner** — which team/system owns this source, in case of questions later.

## Batch vs streaming
- **Batch ingestion** — data pulled on a schedule (hourly, daily). Simpler, cheaper, fine when near-real-time isn't required.
- **Streaming ingestion** — data pushed continuously (Kafka, Kinesis, Pub/Sub). Needed when downstream use cases require low latency (fraud detection, live dashboards).
- **CDC (Change Data Capture)** — a middle ground: captures row-level changes from a source database near-real-time without full batch reloads. Common when the source is an operational database that must stay in sync with the analytics platform.

Decide per source, not once for the whole platform — some sources genuinely need streaming, others don't, and forcing everything into one pattern adds unnecessary complexity.

## Standard ingestion architecture elements
- **Source system icon** — one shape per source type (database, API, file, stream).
- **Ingestion tool/connector** — the tool moving data (e.g. a CDC tool, an ETL connector, a stream consumer).
- **Landing zone** — where raw data lands first, before any transformation (often called the "raw" or "bronze" area — see the data modeling reference for layer naming).

## Representation in Penpot
Frame `01-Source-Ingestion`: a source inventory table at the top (or as a separate linked frame if the list is long), and a diagram below showing each source → its ingestion method → the landing zone. Use distinct icons/colors per source type (database vs API vs file vs stream) so the ingestion pattern is readable at a glance.

## Polish checklist
- [ ] Every source has its update pattern and access method stated, not left implicit
- [ ] Batch, streaming, and CDC are visually distinguished (different arrow style or icon), not drawn identically
- [ ] The landing zone is clearly shown as the single destination for all ingestion paths
