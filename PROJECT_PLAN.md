# Comparative Machine Learning Models for Diabetes Progression and Breast Tumor Classification — Project Plan

## Goal

Apply and compare five machine-learning methods across two biomedical tasks while demonstrating correct cross-validation, preprocessing, independent-test use, model interpretation, and reproducible scientific communication.

## Fixed Datasets and Targets

| Task | Dataset | Split | Primary metric | Models |
|---|---|---|---|---|
| Regression | `sklearn.datasets.load_diabetes` | 80/20, `random_state=42`, shuffled 5-fold CV | RMSE | Linear regression, decision tree, random forest, MLP |
| Classification | `sklearn.datasets.load_breast_cancer` | 80/20, `random_state=42`, stratified 5-fold CV | ROC AUC | Logistic regression, decision tree, random forest, MLP |

For classification, malignant is the positive class (`1`) and benign is the negative class (`0`).

## Execution Sequence

### Phase 1 — Setup and data understanding

- [ ] Record Python and package versions.
- [ ] Confirm both datasets, sample counts, feature counts, target meanings, missing values, and class balance.
- [ ] Produce at least two informative visualizations for each dataset.
- [ ] Create the 80/20 development/test split with `random_state=42`.
- [ ] Stratify the breast-cancer split.
- [ ] Set aside the test set and use it only once for final evaluation.

Deliverables: EDA and preprocessing sections in the notebooks; dataset notes and source information.

### Phase 2 — Regression experiment

- [ ] Use `Pipeline` objects for all data-dependent preprocessing.
- [ ] Train ordinary linear regression as the baseline.
- [ ] Tune decision tree, random forest, and MLP regressors with development 5-fold shuffled `KFold`.
- [ ] Search:
  - decision tree: `max_depth`, `min_samples_leaf`;
  - random forest: `n_estimators`, `max_depth`;
  - MLP: `hidden_layer_sizes`, `alpha`.
- [ ] Report cross-validation MSE, RMSE, MAE, and R² means and standard deviations.
- [ ] Refit selected configurations on all development data and evaluate once on the test set.
- [ ] Create observed-versus-predicted and residual plots for the CV-selected best model.
- [ ] Determine the recommended model from development results, not test ranking.

Deliverable: `notebooks/regression.ipynb`.

### Phase 3 — Classification experiment

- [ ] Recode malignant as `1` and benign as `0`.
- [ ] Use `Pipeline` objects for all data-dependent preprocessing.
- [ ] Tune logistic regression, decision tree, random forest, and MLP classifiers.
- [ ] Search logistic regression `C` and the required nonlinear hyperparameters.
- [ ] Use stratified 5-fold cross-validation and ROC AUC as the selection metric.
- [ ] Report accuracy, precision, recall, F1, and ROC AUC means and standard deviations.
- [ ] Refit selected configurations and evaluate once on the test set.
- [ ] Create the selected model confusion matrix and an independent-test ROC curve for all classifiers.

Deliverable: `notebooks/classification.ipynb`.

### Phase 4 — Complexity experiments

- [ ] Decision trees: evaluate depths `1, 2, 3, 4, 5, 7, 10, and None` using Dataset A.
- [ ] Record development training RMSE and mean 5-fold CV RMSE for every depth.
- [ ] Plot training and CV RMSE versus depth; treat `None` categorically.
- [ ] MLP: fix Dataset B architecture to one hidden layer with 50 neurons.
- [ ] Evaluate `alpha` values `0.0001, 0.001, 0.01, 0.1, and 1.0`.
- [ ] Record development training and CV ROC AUC and plot against `alpha` on a logarithmic axis.
- [ ] Use no independent-test data in these experiments.
- [ ] Check MLP convergence warnings and document optimization adjustments.

Deliverables: complexity figures in `results/figures/` and interpretations in the notebooks/report.

### Phase 5 — Interpretation

- [ ] Examine and interpret linear regression coefficients.
- [ ] Examine and interpret logistic regression coefficients.
- [ ] Account for standardization and correlated predictors when comparing coefficients.
- [ ] Calculate permutation importance for the selected final model in each task using development data.
- [ ] Identify three important predictors for each task.
- [ ] Discuss at least two biologically plausible predictor relationships per task.
- [ ] State that predictive importance does not establish causation.
- [ ] Compare linear versus nonlinear performance and discuss limitations.

Deliverables: interpretation sections in both notebooks and the final report.

### Phase 6 — Scientific report

- [ ] Introduction: research objectives and biological motivation.
- [ ] Data and methods: datasets, splitting, preprocessing, CV, tuning, metrics, and seeds.
- [ ] Results: CV tables, test tables, required figures, and complexity experiments.
- [ ] Discussion: performance, complexity, feature importance, biological relevance, and limitations.
- [ ] Conclusions: concise findings and model recommendations.
- [ ] References: dataset sources and supporting scientific literature.
- [ ] Target length: approximately 5–7 pages excluding references and appendices.
- [ ] Export a final PDF in `report/`.

### Phase 7 — Presentation

- [ ] Create 4–5 slides covering objectives, datasets, methods, key results, and conclusions.
- [ ] Present in approximately 5 minutes.
- [ ] Save the slide deck in `presentation/`.

## Required Methodological Controls

- Use `random_state=42` for splits and applicable randomized methods.
- Use shuffled 5-fold `KFold` for regression and stratified 5-fold `StratifiedKFold` for classification.
- Use scikit-learn pipelines for every data-dependent preprocessing step.
- Fit preprocessing parameters only inside training folds.
- Do not use test data for feature selection, preprocessing decisions, tuning, or model selection.
- Refit every selected model on the complete development set before one independent-test evaluation.
- Document search grids and selection metrics.
- Prefer ROC AUC from probabilities or decision scores, never hard classifications.
- Use 0.5 as the classification threshold unless development-only justification supports another threshold.
- Check MLP convergence and record settings.
- Run both notebooks from start to finish.

## Repository Map

```text
.
├── PROJECT_PLAN.md
├── README.md
├── requirements.txt
├── notebooks/
│   ├── regression.ipynb
│   └── classification.ipynb
├── report/
│   └── track-a-report.pdf
├── presentation/
│   └── track-a-presentation.*
├── results/
│   ├── figures/
│   └── tables/
└── ignore/
    └── Track A project description.pdf
```

## Quality Checklist

- [ ] Both notebooks execute from beginning to end.
- [ ] Development/test separation is evident in code and text.
- [ ] Every tuning search has a documented search space and selection metric.
- [ ] Cross-validation and test tables include the required metrics.
- [ ] All required figures are present and labeled.
- [ ] Biological interpretations distinguish prediction from causation.
- [ ] Report is within its requested page range.
- [ ] Presentation is 4–5 slides and approximately 5 minutes.
- [ ] README lists exact setup and execution instructions.
- [ ] No unnecessary intermediate files or large generated outputs are committed.
