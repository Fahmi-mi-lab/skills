# Serving & Inference Architecture

## What this covers
How a trained, registered model actually produces predictions for real use — this is where ML system design overlaps heavily with general software system design (see the software-system-design skill for deployment/scaling notation if needed).

## Serving patterns
- **Batch inference** — predictions computed on a schedule for a whole dataset, results stored for later use (e.g. nightly churn scores written to a table). Simple, cost-efficient, fine when predictions don't need to reflect the latest input instantly.
- **Online/real-time inference** — a model served behind an API endpoint, returning a prediction per request with low latency. Needed when a prediction must reflect the most current input (e.g. fraud check at checkout).
- **Streaming inference** — predictions computed continuously on a data stream (e.g. real-time anomaly detection on sensor data).

Choose per use case based on the latency requirement clarified in stage 1 — don't default to real-time serving if batch is sufficient, since it adds unnecessary infrastructure complexity and cost.

## Standard serving architecture elements
- **Model serving endpoint** — the service hosting the model (a dedicated model server, a containerized service, or a managed cloud ML endpoint).
- **Feature retrieval at inference time** — how the serving path fetches the same features used in training (ideally from the same feature store referenced in stage 2, to avoid training-serving skew).
- **Pre/post-processing** — any transformation applied to the raw input before it reaches the model, and to the model's raw output before it's returned to the caller.
- **Fallback strategy** — what happens if the model service is unavailable or too slow (return a cached/default prediction, fall back to a simpler heuristic, or fail the request) — this should be a deliberate decision, not an afterthought.

## Representation in Penpot
Frame `05-Serving-Inference`: a diagram showing the request path from caller → pre-processing → feature retrieval (pointing back to the feature store from stage 2) → model endpoint → post-processing → response, with the fallback path shown as a branch. If serving is batch, show the scheduled job → storage → downstream consumer path instead.

## Polish checklist
- [ ] The serving pattern (batch/online/streaming) is stated explicitly and matches the latency requirement from stage 1
- [ ] Feature retrieval at inference time is shown connecting back to the same feature store used in training
- [ ] A fallback path is shown for cases where the model service fails or is too slow
- [ ] Pre/post-processing steps are shown as distinct stages, not hidden inside the model box
