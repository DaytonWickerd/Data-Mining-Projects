# Heart Disease Exploratory Data Analysis

Exploratory data analysis on the UCI Heart Disease dataset to identify which physiological and clinical attributes are most associated with heart disease severity. All statistical functions are implemented from scratch — no scikit-learn or scipy.

---

## Dataset

- **Source:** [UCI Machine Learning Repository — Heart Disease](https://archive.ics.uci.edu/dataset/45/heart+disease)
- **Subset:** Processed Cleveland (303 patients, 13 features)
- **Target:** Disease severity on a 0–4 integer scale (0 = no disease, 1–4 = increasing severity)

Features include both demographic attributes (age, sex) and clinical measurements derived from a standard exercise stress test (maximum heart rate, ST-segment depression, exercise-induced angina) as well as resting values (blood pressure, cholesterol).

---

## Key Findings

- **`thalach` (max heart rate) drives the most negative covariance:** All five feature pairs with negative estimated covariance involve `thalach`. Higher peak exercise heart rate co-varies negatively with age, cholesterol, resting blood pressure, ST depression, and calcified vessel count — consistent with it being a direct marker of cardiovascular health.

- **Top 5 features by variance capture 99.86% of total variance:** The five highest-variance features account for nearly all measured spread in the dataset. This is dominated by measurement scale (cholesterol in mg/dL, blood pressure in mm Hg) rather than clinical importance, underscoring why normalization is essential before any variance-sensitive analysis.

- **No feature pairs have correlation ≥ 0.5:** The strongest pairwise correlation among numerical features is age–ca at r ≈ 0.36. The low collinearity means each feature contributes relatively independent information — a favorable property for predictive modeling.

- **Smallest correlation is age–thalach (r = −0.394):** This is the most negative linear relationship in the data, capturing the well-known physiological decline of maximum exercise heart rate with age.

- **Missing data is minimal and concentrated:** Only `ca` (4 values) and `thal` (2 values) have missing entries, totaling 0.14% of all cells. These are handled via mean imputation.

---

## Statistical Functions Implemented from Scratch

| Function | Description |
|---|---|
| `multidim_mean` | Column-wise mean vector |
| `sample_variance` | Bessel-corrected sample variance |
| `sample_covariance` | Bessel-corrected pairwise covariance |
| `covariance_matrix` | Full symmetric covariance matrix |
| `correlation_coefficient` | Pearson correlation |
| `zscore_normalize` | Standardize to zero mean, unit variance |
| `range_normalize` | Min-max scale to [0, 1] |
| `compute_covariance_matrix` | Covariance over expanded feature matrix |
| `label_encode` | Integer encoding of categorical columns |

---

## Tech Stack

- Python 3
- NumPy
- pandas
- Matplotlib
- JupyterLab

---

## How to Run

```bash
# 1. Clone the repo
git clone https://github.com/<your-username>/data-mining-projects.git
cd data-mining-projects/01-heart-disease-eda

# 2. Install dependencies
pip install -r requirements.txt

# 3. Launch the notebook
jupyter lab notebook.ipynb
```

The notebook reads data from `data/processed_cleveland.data` and saves figures to `figures/`. Both directories are included in the repo.

---

## Project Structure

```
01-heart-disease-eda/
├── notebook.ipynb          # Main analysis notebook
├── requirements.txt
├── data/
│   └── processed_cleveland.data   # Raw UCI Cleveland subset
└── figures/
    ├── missing_values.png
    ├── scatter_plots_3f.png
    ├── scatter_3g.png
    ├── scatter_3h.png
    └── scatter_3i.png
```
