# Problem Framing & Success Metric

## What this covers
The foundation for every ML decision that follows. A model can be technically excellent and still fail the project if it's solving a poorly framed problem or optimizing the wrong metric.

## Problem framing
- **Business problem** — what real-world decision or action does this ML system inform? Write it in plain language, not ML jargon (e.g. "reduce customer churn" not "binary classification task").
- **ML task type** — translate the business problem into a concrete ML task: classification, regression, ranking, clustering, recommendation, generation, forecasting, anomaly detection, etc.
- **Prediction target** — exactly what is being predicted, at what granularity (per user? per transaction? per day?), and at what point in time relative to when the prediction is used.
- **Baseline** — what happens today without ML (a simple heuristic, a manual process, no solution at all)? The ML system must be compared against this baseline, not just against "better than nothing".

## Success metrics
Separate two kinds of metrics — conflating them is a common mistake:
- **Model/offline metric** — how the model is evaluated on held-out data (accuracy, precision/recall, F1, AUC, RMSE, MAP@K, etc., chosen based on task type and class balance).
- **Business/online metric** — the real-world outcome the model is meant to improve (e.g. churn rate reduction, revenue lift, click-through rate), measured after deployment, often via an A/B test.

A good offline metric improvement doesn't guarantee a business metric improvement — state explicitly how the two are expected to connect.

## Constraints to clarify with the user
- Available labeled data (how much, how it was labeled, known biases)
- Latency requirement for a prediction (real-time under X ms, or batch overnight)
- Interpretability requirement (does a human need to explain individual predictions, e.g. for regulatory reasons)
- Acceptable error trade-off (is a false positive worse than a false negative for this use case, or vice versa)

## Representation in Penpot
Frame `01-Problem-Framing`: a short problem statement block, a table separating offline vs online metrics, and a small "baseline vs target" comparison. This is primarily textual — no complex diagram needed.

## Polish checklist
- [ ] The business problem is stated in plain language before any ML terminology is introduced
- [ ] Offline and online/business metrics are clearly separated, not merged into one line
- [ ] A baseline is named explicitly, not left implicit
- [ ] At least one constraint (latency, interpretability, or error trade-off) is addressed if relevant to the use case
