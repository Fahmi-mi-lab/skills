# Training & Evaluation Pipeline

## What this covers
How the model actually gets trained in a reproducible, trackable way, and how it's evaluated before being trusted for deployment.

## Training pipeline elements
- **Experiment tracking** — logging hyperparameters, metrics, and artifacts for every training run (so results are comparable and reproducible), typically via a tool like MLflow, Weights & Biases, or similar.
- **Hyperparameter tuning** — the search strategy used (grid search, random search, Bayesian optimization), and what's being optimized for.
- **Model versioning & registry** — every trained model that passes evaluation gets a version and is stored in a model registry, not just saved as a loose file.
- **Reproducibility** — the training pipeline should be able to reproduce a given model version from its recorded code version, data version, and hyperparameters.

## Evaluation plan
- **Offline evaluation** — metrics computed on the held-out test set (defined in stage 1), broken down by relevant segments (e.g. performance by user region, by data recency) to catch subgroup weaknesses that an aggregate metric would hide.
- **Error analysis** — reviewing a sample of the model's mistakes to understand failure patterns, not just looking at the aggregate score.
- **Fairness/bias check** — if the model affects people, check for performance disparities across sensitive groups where applicable and relevant to the use case.
- **Champion/challenger comparison** — a new model version should be compared against the currently deployed model (the "champion"), not evaluated in isolation.

## Representation in Penpot
Frame `04-Training-Evaluation`: a pipeline diagram showing data (from stage 2) → training job → experiment tracking → evaluation → model registry, with a decision point ("passes evaluation threshold?") before a model is allowed into the registry. Include a small evaluation summary table (metric, segment, champion vs challenger score) alongside the diagram.

## Polish checklist
- [ ] The decision point for promoting a model to the registry is shown explicitly (not implied)
- [ ] Evaluation is broken down by at least one meaningful segment, not just an aggregate score
- [ ] Champion vs challenger comparison is included if a previous model version exists
- [ ] Experiment tracking and model registry are shown as distinct components, not merged into one box
