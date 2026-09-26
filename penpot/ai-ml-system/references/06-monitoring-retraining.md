# Monitoring, Drift & Retraining Loop

## What this covers
A model's performance degrades over time as the real world changes — this stage closes the loop by detecting that degradation and triggering retraining, turning the system into a continuously maintained loop rather than a one-time deployment.

## What to monitor
- **Model performance metrics** — the same offline metrics from stage 4, now measured against live outcomes as they become available (e.g. did the predicted churner actually churn?). Note that ground truth may arrive with a delay — account for that lag in the monitoring design.
- **Prediction distribution** — is the model's output distribution shifting over time (e.g. suddenly predicting far more positives than usual)? This can signal a problem before ground truth is even available.
- **Data/feature drift** — are the input feature distributions changing compared to training data (e.g. a feature's average value shifting significantly)? This is often the earliest warning sign of an upcoming performance drop.
- **System health metrics** — standard software metrics for the serving endpoint: latency, error rate, throughput (see the software-system-design skill's observability reference for the general pattern).

## Drift types (be specific, not just "drift")
- **Data drift** — the distribution of input features changes.
- **Concept drift** — the relationship between inputs and the target changes (the same input now leads to a different outcome than it used to).
- Distinguishing the two matters because the fix differs: data drift may just need re-normalization or new training data; concept drift means the model's learned pattern is genuinely outdated.

## Retraining loop
- **Trigger** — what causes a retraining run: a schedule (e.g. monthly), a performance threshold breach, or a significant drift signal. State which trigger(s) apply.
- **Retraining pipeline reuse** — the retraining run should reuse the same training pipeline from stage 4 (same code path), not a separate ad-hoc process, to guarantee consistency.
- **Redeployment decision** — a retrained model still goes through the same evaluation and champion/challenger comparison from stage 4 before replacing the currently served model — retraining does not mean automatic redeployment.

## Representation in Penpot
Frame `06-Monitoring-Retraining`: a loop diagram — serving (from stage 5) → monitoring (performance, drift, system health) → a decision point ("threshold breached?") → retraining pipeline (pointing back to stage 4) → evaluation → redeployment back into serving. Drawing this as a closed loop (not a straight line) helps communicate that this is an ongoing cycle, not a one-time flow.

## Polish checklist
- [ ] The diagram is drawn as a closed loop, visually distinct from the earlier one-directional pipeline diagrams
- [ ] Data drift and concept drift are distinguished, not lumped into one generic "drift" box
- [ ] The retraining trigger(s) are stated explicitly (schedule, threshold, or drift signal)
- [ ] The redeployment decision point shows that a retrained model must pass evaluation before replacing the live model
