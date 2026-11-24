# Comparative Machine Learning Models for Diabetes Progression and Breast Tumor Classification

Final project for **BINF 6210/8210: Machine Learning for Bioinformatics** at UNC Charlotte.

The project applies and compares linear regression, logistic regression, decision trees, random forests, and multilayer perceptrons (MLPs) on two biomedical prediction problems from scikit-learn:

- **Regression:** predict diabetes disease progression using the Diabetes dataset.
- **Binary classification:** classify malignant versus benign breast tumors using the Wisconsin Diagnostic Breast Cancer dataset.

The goal is to evaluate generalization, model complexity, overfitting, preprocessing, and interpretability—not only to maximize predictive performance.

## Research Questions

### Diabetes progression

How accurately can baseline clinical measurements predict diabetes disease progression one year after baseline?

Models: linear regression, decision tree regression, random forest regression, and MLP regression.

### Breast tumor classification

How accurately can quantitative cell nucleus measurements classify breast tumors as malignant or benign?

Models: logistic regression, decision tree classification, random forest classification, and MLP classification.

For this project, malignant tumors are the positive class (`1`) and benign tumors are the negative class (`0`).

## Project Workflow

1. Perform exploratory data analysis for both datasets.
2. Split each dataset into 80% development data and 20% independent test data with `random_state=42`.
3. Stratify the breast-cancer classification split.
4. Build scikit-learn pipelines to perform all learned preprocessing within cross-validation folds.
5. Tune models using development data only:
   - shuffled 5-fold cross-validation for regression;
   - stratified 5-fold cross-validation for classification.
6. Refit the selected configurations on the full development set.
7. Evaluate each final configuration once on the independent test set.
8. Compare linear and nonlinear methods, investigate complexity and overfitting, and interpret important features.

## Deliverables

- `notebooks/regression.ipynb`: diabetes regression notebook.
- `notebooks/classification.ipynb`: breast cancer classification notebook.
- A 5–7-page scientific PDF report, excluding references and appendices.
- A 4–5-slide, 5-minute presentation.
- This README: setup, environment, and execution instructions.

## Repository Structure

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

See [PROJECT_PLAN.md](/Users/sergimaslinikov/Documents/GitHub/ML_track_A/PROJECT_PLAN.md) for the phase-by-phase checklist and required outputs.

## Requirements

- Python 3
- Jupyter Notebook or JupyterLab
- NumPy
- pandas
- matplotlib
- seaborn
- scikit-learn

Example environment setup:

```bash
python3 -m venv .venv
source .venv/bin/activate
python -m pip install --upgrade pip
python -m pip install -r requirements.txt
```

## Running the Notebooks

```bash
jupyter lab
```

Open and run `notebooks/regression.ipynb` and `notebooks/classification.ipynb` from beginning to end. The notebooks use datasets distributed with scikit-learn, so no external dataset download is required.

## Modeling Details

### Regression

- Primary baseline: ordinary linear regression
- Nonlinear models: decision tree, random forest, and MLP regressors
- Primary model-selection metric: RMSE
- Additional metrics: MSE, MAE, and R²
- Cross-validation: shuffled 5-fold `KFold` with `random_state=42`

### Classification

- Primary baseline: logistic regression
- Nonlinear models: decision tree, random forest, and MLP classifiers
- Primary model-selection metric: ROC AUC
- Additional metrics: accuracy, precision, recall, F1 score, and ROC AUC
- Cross-validation: 5-fold stratified `StratifiedKFold` with `random_state=42`
- Positive class: malignant
- Probability threshold: 0.5, unless an alternative threshold is justified using development data only

### Hyperparameters and Complexity

Regression tuning should include:

- Decision tree: `max_depth`, `min_samples_leaf`
- Random forest: `n_estimators`, `max_depth`
- MLP: `hidden_layer_sizes`, `alpha`

Classification tuning should include:

- Logistic regression: `C`
- Decision tree: `max_depth`, `min_samples_leaf`
- Random forest: `n_estimators`, `max_depth`
- MLP: `hidden_layer_sizes`, `alpha`

Additional required complexity experiments:

- Decision tree regression depths: `1, 2, 3, 4, 5, 7, 10, None`
- MLP classification regularization: `alpha` values `0.0001, 0.001, 0.01, 0.1, 1.0`, using one hidden layer of 50 neurons

## Required Evaluation Outputs

- Cross-validation and independent-test performance tables for all algorithms.
- Observed-versus-predicted and residual plots for the best regression model.
- A confusion matrix and independent-test ROC curve for the classifiers.
- Training and cross-validation complexity plots for the required tree and MLP experiments.
- Linear/logistic coefficients and permutation importance for the development-set-selected final models.
- Biological interpretation of at least two important predictors from each dataset.

## Reproducibility

- Set `random_state=42` for splitting and randomized methods where applicable.
- Use scikit-learn `Pipeline` objects for every preprocessing workflow.
- Fit preprocessing parameters only on training folds.
- Use development data exclusively for preprocessing decisions, feature selection, tuning, model selection, and complexity experiments.
- Evaluate the independent test set only once after model selection.
- Document Python package versions and all relevant model settings.
- Check MLP convergence warnings and document any convergence adjustments.
- Keep code and generated reports or figures reproducible and avoid unnecessary intermediate files.

## Scientific Interpretation

The project emphasizes a scientifically grounded comparison of model assumptions and generalization behavior. Results should discuss:

- linear versus nonlinear performance;
- overfitting and underfitting;
- the effect of standardization and regularization;
- cross-validation versus independent-test performance;
- feature importance and biological plausibility;
- limitations of the datasets and analysis; and
- why predictive importance does not establish causation.

Neither dataset represents a validated clinical prediction system. Additional independent validation, external cohorts, and clinical evaluation would be required before biomedical or clinical use.

## Dataset Documentation

- [Diabetes dataset](https://scikit-learn.org/stable/modules/generated/sklearn.datasets.load_diabetes.html)
- [Breast cancer dataset](https://scikit-learn.org/stable/modules/generated/sklearn.datasets.load_breast_cancer.html)

## Grading Summary

| Component | Points |
|---|---:|
| Exploratory analysis and preprocessing | 15 |
| Regression modeling | 20 |
| Classification modeling | 20 |
| Model complexity and overfitting | 20 |
| Model comparison and interpretation | 15 |
| Scientific communication and reproducibility | 10 |
| **Total** | **100** |

