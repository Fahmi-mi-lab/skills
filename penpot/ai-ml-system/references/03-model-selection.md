# Model / Algorithm Selection

## What this covers
Choosing and justifying the modeling approach — this should follow directly from the problem framing (stage 1) and the data available (stage 2), not be picked first and justified after the fact.

## Selection criteria to weigh explicitly
- **Task fit** — does the algorithm family match the ML task type (e.g. gradient boosting for tabular classification, a sequence model for time-series/text, a neural network for unstructured data like images).
- **Data volume & quality** — some approaches need large labeled datasets (deep learning); others work well with smaller/tabular data (tree-based models, linear models).
- **Interpretability requirement** — if predictions must be explainable (e.g. for regulatory or trust reasons), simpler/interpretable models or explainability tooling (SHAP, LIME) may be required over a black-box model.
- **Latency & resource constraints** — a highly accurate but computationally heavy model may not fit a real-time low-latency serving requirement.
- **Build vs use existing** — consider whether a pre-trained/foundation model (fine-tuned or used via API) is more appropriate than training a model from scratch, especially for tasks like NLP or vision where strong pre-trained models already exist.

## Model comparison table
Compare at least 2-3 candidate approaches side by side before committing:

| Approach | Task fit | Data requirement | Interpretability | Latency | Notes |
|----------|----------|-------------------|-------------------|---------|-------|
| ... | ... | ... | ... | ... | ... |

## Justification (mini-ADR style)
For the chosen approach, write briefly:
- **Decision** — which approach was chosen
- **Why** — which criteria above tipped the decision
- **Rejected alternatives** — what else was considered and why it wasn't chosen
- **Risks** — known limitations of the chosen approach (e.g. may need frequent retraining, may not generalize to a new user segment)

## Representation in Penpot
Frame `03-Model-Selection`: the comparison table as the main element, with a short justification block below it. This is primarily textual — no complex diagram needed, though a simple decision-tree-style visual can be used if there were multiple decision branches worth showing.

## Polish checklist
- [ ] At least two alternative approaches are compared, not just the chosen one presented alone
- [ ] The justification explicitly ties back to the problem framing and data constraints from earlier stages
- [ ] Known risks/limitations of the chosen approach are stated, not omitted
