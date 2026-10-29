# Ames Housing Price Prediction

A compact regression study using the Ames Housing dataset to compare a simple
baseline, a larger linear model, and Lasso regularization. The notebook covers
data inspection, preprocessing, feature selection, evaluation, and residual
diagnostics.

> **Status:** educational data-science project. The reported numbers come from
> one reproducible train/test split and should not be interpreted as production
> performance or as a benchmark against state-of-the-art housing models.

## Results

The target is log-transformed `SalePrice`. The notebook reports:

| Model | Features | Train R² | Test R² | Test MSE |
|---|---:|---:|---:|---:|
| Linear Regression | 10 selected | 0.798 | 0.835 | 0.028 |
| LassoCV | automated selection | 0.725 | 0.798 | 0.034 |
| Linear Regression | 2 | 0.719 | 0.775 | 0.038 |

The 10-feature model produced the strongest test score in this split. Its test
R² being higher than its train R² does **not** prove the absence of overfitting;
the difference can arise from sampling variation. Repeated cross-validation or
an untouched external test set would provide stronger evidence.

## Workflow

1. Load the public `house_prices` dataset through `fetch_openml`.
2. Inspect missing values, distributions, and correlations.
3. Log-transform the target to reduce skew.
4. Establish a two-feature linear-regression baseline.
5. Fit a 10-feature linear model and a `LassoCV` model.
6. Compare MSE and R² on a fixed split (`random_state=42`).
7. Inspect residual plots and a Q–Q plot for model-assumption diagnostics.

Residual diagnostics are evidence to inspect, not a guarantee that all linear
model assumptions hold. Tail deviations indicate that unusual properties remain
harder to represent with a simple linear specification.

## Reproduce the notebook

Python 3.11 is recommended.

```bash
git clone https://github.com/alikhrzh/Ames-housing-prices-prediction.git
cd Ames-housing-prices-prediction
python -m venv .venv
source .venv/bin/activate
python -m pip install -r requirements.txt
jupyter lab Ames_Housing_Price_Prediction.ipynb
```

The first data-loading step requires network access to OpenML. Restart the
kernel and run all cells from top to bottom when validating the results.

## Repository structure

```text
Ames_Housing_Price_Prediction.ipynb  complete analysis and model comparison
requirements.txt                    reproducibility dependencies
README.md                           results, workflow, and limitations
LICENSE                             MIT license for the project code
```

This is intentionally a notebook-sized educational repository:

- `Ames_Housing_Price_Prediction.ipynb` contains data loading, inspection,
  preprocessing, feature analysis, model fitting, metrics, and residual plots
  in one executable narrative.
- `requirements.txt` declares the Python packages needed to reproduce the
  notebook; the dataset itself is fetched from OpenML rather than committed.
- `README.md` reports the saved results and their interpretation without
  treating one train/test split as a production benchmark.

If the project grows, the next structural step should be a leakage-safe
preprocessing pipeline in `src/` plus an automated evaluation script and tests.
The current size does not justify those extra layers yet.

## Limitations and next steps

- Results currently use one train/test split rather than repeated nested cross-validation.
- Feature selection is partly informed by exploratory correlation analysis.
- The study does not compare tree-based or boosting baselines.
- No prediction-interval or subgroup error analysis is included.
- The notebook retains outputs for review; a clean automated execution check is not yet configured.

Useful next experiments are a leakage-safe preprocessing pipeline, repeated
cross-validation, comparison with gradient boosting, and error analysis by
property price range.

## License

The project code is available under the MIT License. The dataset is retrieved
from OpenML and remains subject to its source metadata and terms.
