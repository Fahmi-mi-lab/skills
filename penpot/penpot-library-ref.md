# Penpot Library Reference

This file documents the shared Penpot library (colors, text styles, and components) that all three system-design skills rely on. Build these in a dedicated Penpot file, publish it as a shared library, and link it into every project file before running a skill.

## Colors (Assets → Colors)

| Token | Used for |
|---|---|
| `brand-primary` | Primary system/service boxes (C4 container, model box) |
| `external-muted` | External/third-party systems |
| `db-accent` | Any database representation, across all three domains |
| `neutral-fill` | Default fill for generic shapes |
| `neutral-border` | Default stroke/border |
| `boundary-dashed` | Network boundary / grouping frames |
| `alert-accent` | SPOF, error, warning highlights |
| `layer-bronze` / `layer-silver` / `layer-gold` | Medallion layer bands (data engineering) |
| `stage-data` / `stage-training` / `stage-serving` | Pipeline stage boxes (AI/ML) |
| `label-text` | Body/label text inside shapes |
| `label-title` | Frame title text |

## Typography (Assets → Typographies)

| Style | Used for |
|---|---|
| `title-frame` | Frame titles |
| `label-component` | Text inside components |
| `caption-note` | Small annotations/checklists |

## Components — build these first (shared across all three skills)

Plain components (fixed structure, no variant needed):

| Component | Structure |
|---|---|
| `common/process-box` | Board (Flex), fill `neutral-fill`, border `neutral-border`, one centered text layer (`label-component`) |
| `common/decision-diamond` | Diamond shape + centered text layer (fixed position, not flex) |
| `common/start-end-oval` | Pill/oval shape + centered text layer |
| `common/database-cylinder` | Cylinder shape + text label below |
| `common/actor-icon` | Person icon + text label below |
| `common/network-boundary-frame` | Large dashed-border board with a corner label |
| `common/arrow-sync` / `common/arrow-async` | Connector styles, not boxes — define as stroke styles or connector presets |

## Components — variant families

Build these as ONE component each with a variant property, not as separate lookalike components:

| Component family | Variant property | Values | Notes |
|---|---|---|---|
| `system-box` | `scope` | `internal`, `external` | Same box structure; `external` uses dashed border + `external-muted` fill |
| `data/source-icon` | `type` | `db`, `api`, `file`, `stream` | Same structure (icon + label below); swap the nested icon per value |
| `data/layer-band` | `layer` | `bronze`, `silver`, `gold` | Same band structure; fill and label text change per value |
| `ai/stage-box` | `stage` | `data`, `training`, `serving` | Same box structure; fill and label text change per value |
| `software/attribute-row` | `kind` | `none`, `pk`, `fk` | Used inside `software/entity-box`; badge style changes per value |

## Components — domain-specific structured components

| Component | Structure |
|---|---|
| `software/container-box` | Board (Flex): title text row + technology label row |
| `software/entity-box` | Board (Flex, vertical, resize-to-fit): header sub-board (entity name) + N nested instances of `software/attribute-row` |
| `software/load-balancer-icon` | Icon + label |
| `software/cdn-icon` | Icon + label |
| `software/lifeline` | Vertical dashed line, fixed height set per diagram |
| `software/activation-bar` | Thin vertical rectangle, positioned on a lifeline |
| `data/pipeline-task-box` | Same as `common/process-box`, color-overridden per layer (reuse, don't duplicate) |
| `data/lineage-arrow` | Connector style distinct from `common/arrow-sync`/`arrow-async`, so lineage is visually distinguishable from task-dependency arrows |
| `ai/feature-store-icon` | Icon + label |
| `ai/serving-endpoint-icon` | Icon + label |
| `ai/monitoring-icon` | Icon + label |
| `ai/loop-arrow` | Curved connector style, distinct from linear pipeline arrows |

## Build order

1. 3 base colors (`brand-primary`, `neutral-fill`+`neutral-border`, `alert-accent`) — derive the rest as tints/shades later.
2. 3 text styles.
3. The plain `common/*` components.
4. The variant families (`system-box`, `data/source-icon`, `data/layer-band`, `ai/stage-box`, `software/attribute-row`).
5. Remaining domain-specific structured components, one domain at a time, as you actually use that skill.

## Instruction for agents (MCP execution)

When a skill's SKILL.md calls for a component listed above as a variant family, always set the corresponding variant property explicitly when instantiating it via MCP — never leave it on the component's default variant.
