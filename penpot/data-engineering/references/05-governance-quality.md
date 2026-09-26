# Governance & Data Quality

This stage is often treated as an afterthought, but it's usually the first thing questioned when stakeholders stop trusting the numbers coming out of the platform. It doesn't always need a new diagram — it can be annotations layered on top of the pipeline and storage diagrams already built.

## Data quality dimensions
Standard categories to check for every critical dataset, not just "does it look right":
- **Completeness** — are required fields populated (no unexpected nulls)?
- **Accuracy** — does the data correctly reflect reality (e.g. does a sum match the source system's total)?
- **Consistency** — do the same values match across different tables/systems (e.g. customer ID format the same everywhere)?
- **Timeliness** — does the data arrive within the expected freshness window?
- **Uniqueness** — no unintended duplicate records (e.g. duplicate primary keys).
- **Validity** — does data conform to expected format/range (e.g. a date field actually contains valid dates).

## Data quality checks in the pipeline
- **Schema validation** — enforce expected schema at ingestion, fail or quarantine records that don't match.
- **Automated tests** — assertions run as part of the pipeline (e.g. row count thresholds, null checks, referential integrity checks between fact and dimension tables).
- **Quarantine/dead-letter pattern** — records that fail validation are routed aside for review instead of silently dropped or silently breaking downstream tables.

## Governance
- **Data ownership** — who is accountable for each dataset's correctness (often the source system owner, not the data team).
- **Access control** — who can read/write each layer (e.g. gold layer may be broadly readable, bronze/raw layer restricted).
- **PII/sensitive data handling** — identify which fields are sensitive, whether they need masking/encryption/tokenization, and where that happens in the pipeline (ideally as early as possible, e.g. at ingestion or in the silver layer).
- **Data catalog** — how datasets are documented and discoverable (schema, description, owner, freshness) for other teams.

## Representation in Penpot
Two possible forms:
1. Annotations added to the existing `03-Pipeline-Orchestration` and `04-Storage-Lineage` frames (mark quality-check points on the DAG, flag PII fields in the storage/lineage diagram), or
2. A separate frame `05-Governance-Quality` with a checklist/summary table if annotating directly would make the existing diagrams too cluttered.

Choose based on how much detail is needed — a small project may just need a short checklist frame; a larger or regulated project benefits from explicit annotations at each relevant pipeline stage.

## Polish checklist
- [ ] At least the completeness, accuracy, and timeliness dimensions are addressed for critical datasets
- [ ] Quality check points are shown at specific stages in the pipeline, not stated only as a general principle
- [ ] PII/sensitive fields are explicitly flagged, along with where they get masked/protected
- [ ] Data ownership is stated for at least the most critical datasets
