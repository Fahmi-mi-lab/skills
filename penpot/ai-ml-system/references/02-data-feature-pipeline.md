# Data Pipeline & Feature Engineering

## What this covers
How raw data becomes the features a model actually trains and predicts on. This stage often determines model performance more than the choice of algorithm itself.

## Data pipeline elements
- **Data sources** — same categories as a general data engineering pipeline (databases, event streams, third-party data, logs). If a data-engineering platform already exists in the project, this stage should plug into its gold/curated layer rather than duplicate ingestion.
- **Labeling** — how ground-truth labels are obtained (human annotation, implicit feedback like clicks, weak supervision, existing business records). Note label quality and potential bias.
- **Feature engineering** — transforming raw fields into model-ready features: aggregations, encodings (one-hot, embeddings), normalization/scaling, time-windowed features (e.g. "purchases in last 30 days").
- **Feature store** — a centralized place to compute, store, and serve features consistently between training and inference (avoids "training-serving skew," where features are computed differently in each environment).

## Training-serving skew (a key risk to design against)
The most common cause of ML systems performing well offline but poorly in production is a mismatch between how a feature is computed at training time versus at inference time (e.g. a time-windowed feature computed differently in a batch job vs a real-time service). Explicitly state how this is avoided (shared feature computation logic, feature store, or the same code path used in both environments).

## Data splitting
- **Train / validation / test split** — how data is divided, and whether the split is random or time-based. For most real-world problems with a temporal element, use a **time-based split** (train on the past, validate/test on more recent data) rather than random splitting, to avoid leaking future information into training.

## Representation in Penpot
Frame `02-Data-Feature-Pipeline`: a flow from source/curated data → labeling → feature engineering → feature store → (train set / inference input), using reusable stage boxes. Mark clearly where the feature store sits between training and serving paths to visually reinforce that both paths share the same feature logic.

## Polish checklist
- [ ] The labeling method is stated, including any known bias or limitation
- [ ] Training-serving skew mitigation is explicitly shown (shared feature store or shared logic), not left implicit
- [ ] Train/validation/test split strategy is stated, including whether it's time-based
- [ ] Feature engineering steps are specific (named transformations), not just a generic "feature engineering" box
