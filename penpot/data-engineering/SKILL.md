---
name: data-engineering-system-design
description: Produces a complete data engineering system design (ingestion, data modeling, pipeline/orchestration, storage & lineage, governance & quality) following industry standards, and turns it into structured diagrams in Penpot via MCP.
---

# Data Engineering System Design

## When this skill applies
Trigger when the user asks for: a data pipeline design, a data platform/lakehouse architecture, an ETL/ELT design, a data flow diagram, or a review/creation of how data moves from source to consumption in a project.

## Operating principles
1. This skill is a knowledge scaffold, not an action. It drives the order of thinking and the standards used; visual execution happens through Penpot MCP tools.
2. Don't design the pipeline before the data sources, freshness requirements, and consumption patterns are clear — an elegant pipeline for the wrong latency/volume assumptions is wasted work.
3. Ask the user about things that can't be guessed (data volume, freshness/latency requirements, batch vs real-time need, existing tools/warehouse in use, compliance requirements) before committing to an architecture — never invent these.
4. Prefer reuse: components and styles from the project's Penpot library over new shapes.

## Workflow (mandatory order)
Read the relevant reference file before working on each stage — don't rely on general memory, since each reference contains specific visual conventions that must stay consistent.

| # | Stage | Reference file | Output |
|---|-------|-----------------|--------|
| 1 | Source & Ingestion | `references/01-source-ingestion.md` | Source inventory + ingestion diagram |
| 2 | Data Modeling & Lakehouse Layers | `references/02-data-modeling-layers.md` | Layer diagram (bronze/silver/gold) + schema model |
| 3 | Pipeline & Orchestration | `references/03-pipeline-orchestration.md` | DAG / pipeline diagram |
| 4 | Storage & Lineage | `references/04-storage-lineage.md` | Storage architecture + lineage diagram |
| 5 | Governance & Data Quality | `references/05-governance-quality.md` | Governance/quality checklist & annotations |

Stage 1 includes a textual source inventory (table) in addition to its diagram — keep both in the same frame set so the document stays complete in one file.

## How to execute in Penpot (MCP)
- **Reuse first, draw manually only as a last resort.** Check whether a matching component (source icon, storage layer box, orchestrator node, database/warehouse icon, etc.) already exists in the project's shared library. If it does, instantiate that component via MCP — don't draw a new shape from scratch.
- **Colors and text from tokens, never hardcoded.** Pull from the project's color styles / text styles (e.g. `source-external`, `layer-bronze`, `layer-silver`, `layer-gold`, `label-text`). If a token for a given category doesn't exist yet, create it once and save it to the library — so later stages/diagrams (even in a different session or agent) can reuse it.
- **One frame per stage.** Consistent naming: `[Number]-[Stage-Name]`, e.g. `01-Source-Ingestion`, `03-Pipeline-Orchestration`.
- **Consistent layout:** pick a default flow direction (left→right or top→bottom, following the natural data flow from source to consumption) at the start of the project and keep it across every frame.
- **Check the polish checklist** at the end of each reference file before considering a stage done: alignment to grid, consistent spacing, no overlapping labels, arrows pointing the same direction.

## Final output
One Penpot file with 5 structured frames matching the table above. Narrative/decision content (source inventory, quality rules, governance policies) can be summarized as text inside the Penpot frame or as a companion markdown document — ask the user which they prefer.
