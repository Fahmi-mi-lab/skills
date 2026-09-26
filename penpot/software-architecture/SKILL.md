---
name: software-system-design
description: Produces a complete software system design (architecture, tech stack, data model, flows, deployment, resilience) following industry standards, and turns it into structured diagrams in Penpot via MCP.
---

# Software System Design

## When this skill applies
Trigger when the user asks for: a software architecture design, a system design document, a system diagram, "design the architecture for project X", or a tech stack / data model review or creation for an application/backend/API.

## Operating principles
1. This skill is a knowledge scaffold, not an action. It drives the order of thinking and the standards used; visual execution happens through Penpot MCP tools.
2. Do not jump into drawing diagrams before earlier stages (especially Requirements and Tech Stack) are clear — a good-looking diagram built on wrong assumptions is useless.
3. Always ask the user about things that can't be guessed (expected user scale, team/budget constraints, cloud provider preference) before making big decisions in an ADR — never invent requirements.
4. Prefer reuse: components and styles from the project's Penpot library over new shapes.

## Workflow (mandatory order)
Read the relevant reference file before working on each stage — don't rely on general memory, since each reference contains specific visual conventions that must stay consistent.

| # | Stage | Reference file | Output |
|---|-------|-----------------|--------|
| 1 | Requirements & Constraints | `references/01-requirements-constraints.md` | FR & NFR list/table |
| 2 | High-Level Architecture (C4) | `references/02-c4-model.md` | Context + Container diagram |
| 3 | Tech Stack & ADR | `references/03-tech-stack-adr.md` | Stack table + ADR document |
| 4 | Data Model / ERD | `references/04-data-model-erd.md` | ERD diagram |
| 5 | Sequence / Flow for critical processes | `references/05-sequence-flow.md` | Sequence/flowchart diagram |
| 6 | Deployment & Infrastructure | `references/06-deployment-infra.md` | Deployment diagram |
| 7 | Scalability, Failure Mode, Observability | `references/07-scalability-observability.md` | Resilience annotations/checklist |

Stages 1 and 3 are mostly textual (tables/lists) rather than complex visual diagrams — still give them their own frame in Penpot so the full document lives in one file.

## How to execute in Penpot (MCP)
- **Reuse first, draw manually only as a last resort.** Check whether a matching component (service box, database cylinder, actor icon, etc.) already exists in the project's shared library. If it does, instantiate that component via MCP — don't draw a new shape from scratch.
- **Some components are variant families, not standalone components** (e.g. `system-box` with a `scope: internal/external` property). When instantiating one, always set the correct variant property (don't leave it on the default) — see `penpot-library-ref.md` for which components have variants and what their properties mean.
- **Colors and text from tokens, never hardcoded.** Pull from the project's color styles / text styles (e.g. `service-primary`, `db-fill`, `label-text`). If a token for a given category doesn't exist yet, create it once and save it to the library — so the next stage/diagram (even in a different session or agent) can reuse it.
- **One frame per stage.** Consistent naming: `[Number]-[Stage-Name]`, e.g. `02-High-Level-Architecture`, `04-Data-Model-ERD`.
- **Consistent layout:** pick a default flow direction (left→right or top→bottom) at the start of the project and keep it across every frame.
- **Check the polish checklist** at the end of each reference file before considering a stage done: alignment to grid, consistent spacing, no overlapping labels, arrows pointing the same direction.

## Final output
One Penpot file with 7 structured frames matching the table above. Narrative/decision content (requirements, ADR) can be summarized as text inside the Penpot frame or as a companion markdown document — ask the user which they prefer.
