# Pipeline & Orchestration

## What this covers
How the transformations between layers (bronze → silver → gold) actually get executed, scheduled, and monitored as a pipeline — not just the data model itself.

## Core concepts
- **DAG (Directed Acyclic Graph)** — the standard way to represent a pipeline: a set of tasks with dependencies, where each task runs only after its upstream tasks complete, and there are no circular dependencies.
- **Task/Job** — one unit of work in the pipeline (e.g. "extract from source A", "transform table X", "load into gold").
- **Scheduling** — how often the pipeline runs (cron schedule, event-triggered, continuous streaming job).
- **Idempotency** — a pipeline run should produce the same result if re-run on the same input; this matters for safe retries and backfills. Note explicitly whether each task is idempotent.
- **Backfill** — the ability to reprocess historical data (e.g. after a bug fix), usually a parameterized re-run of the same DAG for past dates.

## Orchestration tool concepts (tool-agnostic)
Regardless of the specific tool (Airflow, Dagster, Prefect, dbt, managed cloud schedulers), the diagram should show:
- **Trigger** — what starts the pipeline (schedule, upstream event, manual trigger).
- **Task dependencies** — which tasks must finish before others start.
- **Failure handling** — retry policy, alerting on failure, and whether a failure blocks downstream tasks or degrades gracefully.

## Representation in Penpot
Frame `03-Pipeline-Orchestration`: draw the DAG left→right or top→bottom, with task boxes connected by arrows showing dependency order. Group tasks by layer (bronze tasks, silver tasks, gold tasks) using background bands or grouping frames so the mapping back to the Data Modeling stage is visually obvious. Mark the trigger/schedule at the start of the DAG.

## Polish checklist
- [ ] Task dependency direction is unambiguous (no crossing arrows that could be misread)
- [ ] The trigger/schedule for the pipeline is shown, not just the tasks
- [ ] Tasks are grouped or color-coded by layer (bronze/silver/gold) to match the data modeling diagram
- [ ] Failure handling / retry behavior is noted for at least the most critical tasks
