---
name: ai-ml-system-design
description: Produces a complete AI/ML system design (problem framing, data pipeline, model selection, training & evaluation, serving, monitoring & retraining) following industry standards, and turns it into structured diagrams in Penpot via MCP.
---

# AI/ML System Design

## When this skill applies
Trigger when the user asks for: an ML system architecture, an AI product design, a model training/serving pipeline diagram, or a review/creation of how a machine learning capability is built, deployed, and maintained in a project.

## Operating principles
1. This skill is a knowledge scaffold, not an action. It drives the order of thinking and the standards used; visual execution happens through Penpot MCP tools.
2. Don't jump to model/algorithm choice before the problem framing and success metric are clear — a well-tuned model solving the wrong problem is wasted work.
3. Ask the user about things that can't be guessed (available labeled data, latency requirements for inference, whether this is batch or real-time prediction, existing ML platform/tools in use, regulatory constraints on the model's decisions) before committing to an architecture — never invent these.
4. Prefer reuse: components and styles from the project's Penpot library over new shapes.

## Workflow (mandatory order)
Read the relevant reference file before working on each stage — don't rely on general memory, since each reference contains specific visual conventions that must stay consistent.

| # | Stage | Reference file | Output |
|---|-------|-----------------|--------|
| 1 | Problem Framing & Success Metric | `references/01-problem-framing.md` | Problem statement + metric definition |
| 2 | Data Pipeline & Feature Engineering | `references/02-data-feature-pipeline.md` | Data/feature pipeline diagram |
| 3 | Model/Algorithm Selection | `references/03-model-selection.md` | Model comparison table + justification |
| 4 | Training & Evaluation Pipeline | `references/04-training-evaluation.md` | Training pipeline diagram + evaluation plan |
| 5 | Serving & Inference Architecture | `references/05-serving-inference.md` | Serving architecture diagram |
| 6 | Monitoring, Drift & Retraining Loop | `references/06-monitoring-retraining.md` | Monitoring/retraining loop diagram |

Stages 1 and 3 are mostly textual (statements/tables) rather than complex visual diagrams — still give them their own frame in Penpot so the full document lives in one file.

## How to execute in Penpot (MCP)
- **Reuse first, draw manually only as a last resort.** Check whether a matching component (data source icon, pipeline stage box, model box, serving endpoint icon, etc.) already exists in the project's shared library. If it does, instantiate that component via MCP — don't draw a new shape from scratch.
- **Some components are variant families, not standalone components** (e.g. `stage-box` with a `stage: data/training/serving` property). When instantiating one, always set the correct variant property (don't leave it on the default) — see `penpot-library-ref.md` for which components have variants and what their properties mean.
- **Colors and text from tokens, never hardcoded.** Pull from the project's color styles / text styles (e.g. `stage-data`, `stage-training`, `stage-serving`, `label-text`). If a token for a given category doesn't exist yet, create it once and save it to the library — so later stages/diagrams (even in a different session or agent) can reuse it.
- **One frame per stage.** Consistent naming: `[Number]-[Stage-Name]`, e.g. `02-Data-Feature-Pipeline`, `05-Serving-Inference`.
- **Consistent layout:** pick a default flow direction (left→right or top→bottom, following the natural flow from raw data to a served prediction) at the start of the project and keep it across every frame.
- **Check the polish checklist** at the end of each reference file before considering a stage done: alignment to grid, consistent spacing, no overlapping labels, arrows pointing the same direction.

## Final output
One Penpot file with 6 structured frames matching the table above. Narrative/decision content (problem statement, model justification, evaluation plan) can be summarized as text inside the Penpot frame or as a companion markdown document — ask the user which they prefer.
