# PCA, Dimensionality Reduction & Clustering

A progressive exploration of Principal Component Analysis and clustering techniques, starting from synthetic 2D data and scaling up to real-world housing datasets. Variance structure and PCA concepts are interpreted manually before applying scikit-learn, and both k-means and DBSCAN are compared to highlight how each method understands cluster structure differently.

---

## What This Project Covers

| Section | Dataset | Techniques |
|---|---|---|
| 1 | Synthetic bivariate normal | Data generation, covariance visualization |
| 2 | Transformed synthetic data | Rotation & scaling transforms, covariance analysis |
| 3 | PCA on transformed data | PCA, variance fractions, decorrelation |
| 4 | Boston Housing (506 × 13) | PCA + k-means + DBSCAN |
| 5 | California Housing (20,640 × 8) | DBSCAN, geographic cluster visualization |

---

## Key Findings

**Effect of rotation and scaling on covariance:**
Applying a scaling matrix S (factors 3 and 4) followed by a 45-degree rotation R transforms a circular normal cloud into a tilted ellipse. The scaling amplifies total variance from ~2 to ~25 (3² + 4² = 25). The rotation introduces off-diagonal covariance terms -- the two dimensions become correlated -- but does not change total variance, because rotation is an orthogonal transformation that preserves norms.

**PCA decorrelates features:**
Applying PCA to the rotation-scaled data recovers axis-aligned principal components. The covariance matrix of the PCA output is diagonal to machine precision -- off-diagonal values are ~1e-13, effectively zero. This confirms PCA's core property: it rotates the data to the eigenvector basis of the covariance matrix, making all principal components uncorrelated.

**7 of 13 Boston features capture 90% of variance:**
After standard normalization, fitting full PCA on the 13-feature Boston dataset shows that 7 principal components are sufficient to retain 90% of the total variance. The scree plot shows a steep initial decline followed by diminishing returns -- a pattern typical of real-world data with substantial feature co-variation. Only 2 components are needed for visualization, but they retain just ~60.9% of the variance.

**K-means vs DBSCAN on Boston data:**
K-means (k=2) splits the PCA-projected Boston neighborhoods into two groups separated along the first principal component -- the dominant axis of variation, likely contrasting high-value suburban areas from densely populated urban ones. DBSCAN identifies the same dense core but explicitly labels sparse outlier neighborhoods as noise rather than forcing them into a cluster. The two algorithms answer different questions: k-means partitions the full population; DBSCAN identifies where natural density concentrations exist.

**DBSCAN reveals California's metropolitan geography:**
Running DBSCAN on the standardized California Housing features and plotting results by longitude and latitude shows that density-based clusters map directly onto California's major metro areas: the Bay Area, Los Angeles, and San Diego emerge as distinct clusters. Rural and sparsely populated areas are classified as noise. This demonstrates DBSCAN's advantage for spatial data -- it discovers arbitrarily shaped, density-driven regions without requiring a pre-specified number of clusters.

---

## Manual vs. sklearn Implementation

Variance explained fractions, covariance matrices, and the trace (total variance) are computed manually using NumPy before using sklearn's PCA. This makes the mathematical relationship between eigenvalues, explained variance, and the PCA rotation explicit before relying on the library abstraction.

---

## Tech Stack

- Python 3
- NumPy
- pandas
- Matplotlib
- scikit-learn (PCA, StandardScaler, KMeans, DBSCAN)
- JupyterLab

---

## How to Run

```bash
# 1. Clone the repo
git clone https://github.com/<your-username>/data-mining-projects.git
cd data-mining-projects/03-pca-dimensionality-reduction

# 2. Install dependencies
pip install -r requirements.txt

# 3. Launch the notebook
jupyter lab notebook.ipynb
```

Data is read from `data/Boston.csv`. The California Housing dataset is downloaded automatically via scikit-learn. All figures are saved to `figures/`.

---

## Project Structure

```
03-pca-dimensionality-reduction/
├── notebook.ipynb
├── requirements.txt
├── data/
│   └── Boston.csv
└── figures/
    ├── bivariate_normal.png
    ├── linear_transformation.png
    ├── pca_transformed.png
    ├── boston_pca_scatter.png
    ├── boston_variance_explained.png
    ├── boston_kmeans.png
    ├── boston_dbscan.png
    └── california_dbscan.png
```
