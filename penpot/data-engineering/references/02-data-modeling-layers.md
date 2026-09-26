# Data Modeling & Lakehouse Layers

## What this covers
How raw data gets progressively cleaned, structured, and modeled into something usable for analytics, reporting, or downstream ML — and the standard layering used to organize that transformation.

## The layered (medallion) architecture
A widely used industry pattern for organizing a lakehouse:
- **Bronze (raw)** — data exactly as ingested, untransformed, kept for reprocessing/audit. No business logic applied.
- **Silver (cleaned/conformed)** — deduplicated, type-cast, validated, joined to reference data. Still close to source structure but usable.
- **Gold (curated/business-level)** — aggregated, modeled specifically for consumption (dashboards, ML features, reporting). This is what most end users query.

Not every project needs all three named exactly this way, but the *progression* — raw → cleaned → business-ready — should always exist in some form, even if named differently.

## Dimensional modeling (for the Gold layer)
When the Gold layer feeds BI/reporting, use standard dimensional modeling concepts:
- **Fact table** — records events/transactions with measurable values (e.g. `fact_orders` with amount, quantity).
- **Dimension table** — descriptive context around facts (e.g. `dim_customer`, `dim_product`, `dim_date`).
- **Star schema** — one fact table surrounded by dimension tables, the standard layout for analytical queries.
- **Slowly Changing Dimensions (SCD)** — note if a dimension needs to track historical changes (SCD Type 2) vs just overwrite (SCD Type 1).

## Representation in Penpot
Frame `02-Data-Modeling-Layers`: three (or however many) vertical or horizontal bands representing bronze/silver/gold, with representative table/dataset boxes inside each band and arrows showing the transformation flow between layers. If a star schema is relevant, add it as a sub-diagram (fact table in the center, dimension tables around it, connected by relationship lines).

## Polish checklist
- [ ] Each layer's purpose (raw / cleaned / business-ready) is labeled, not just named bronze/silver/gold without explanation
- [ ] Arrows between layers indicate the direction of transformation, not just adjacency
- [ ] If a star schema is included, the fact table is visually distinct from dimension tables (e.g. different fill color)
- [ ] SCD type is noted for any dimension where historical tracking matters
