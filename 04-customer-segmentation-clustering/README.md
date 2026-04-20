# Customer Segmentation with PCA & Clustering

Unsupervised learning project applying K-Means and DBSCAN clustering — both implemented from scratch — to the UCI Wholesale Customers dataset, with Principal Component Analysis used to reduce dimensionality before comparing clustering results.

---

## Project Overview

The [UCI Wholesale Customers dataset](https://archive.ics.uci.edu/dataset/292/wholesale+customers) contains 440 records representing clients of a wholesale distributor in Portugal. Each record captures annual spending (in monetary units) across six product categories: **Fresh, Milk, Grocery, Frozen, Detergents_Paper, and Delicassen**. An additional categorical variable — **Channel** (restaurant vs. retail) — provides ground-truth labels used to evaluate clustering quality.

The analysis follows this pipeline:

1. Standardize the six spending features
2. Apply PCA to understand variance structure and select a reduced dimensionality
3. Run K-Means and DBSCAN on both the original (6D) and PCA-reduced (4D) data
4. Compare algorithm performance using the elbow method, parameter grid search, and clustering precision against the ground-truth Channel labels

Both K-Means and DBSCAN are **implemented from scratch** — no sklearn clustering equivalents are used for the core algorithm implementations. Sklearn's `PCA`, `StandardScaler`, and `euclidean_distances` are used for preprocessing and distance computation only.

---

## Key Findings

### PCA
- Four principal components capture **~94% of the total variance** in the standardized data.
- The 2D PCA projection reveals a dense central cluster with scattered outliers but no cleanly separable groups in just two dimensions.

### K-Means
- The elbow method identifies **k = 3** as the optimal number of clusters for both the original and reduced data.
- Three segments emerge: high-Grocery/Detergents_Paper spenders (retail), high-Fresh/Milk spenders (restaurants), and a moderate mixed-spend group.
- K-Means precision against the binary Channel labels reaches approximately **0.85–0.90** at k = 2–3.

### DBSCAN
- DBSCAN struggles on this dataset across all tested parameter combinations.
- Small epsilon values (0.5) produce 2–6 clusters but classify 30–40% of points as noise.
- Larger epsilon values collapse all customers into a single cluster.
- PCA reduction modestly reduces the noise point count but does not resolve the fundamental density overlap.
- **Conclusion:** the customer spending distributions are not well-separated in density space; K-Means is the more appropriate algorithm for this dataset.

### Customer Segment Characteristics
| Segment | Key Spending Pattern | Likely Type |
|---------|---------------------|-------------|
| 1 | High Grocery, Detergents_Paper | Retail stores |
| 2 | High Fresh, Milk | Restaurants / food service |
| 3 | Moderate across all categories | Mixed / small buyers |

---

## Tech Stack

| Tool | Purpose |
|------|---------|
| Python 3.11 | Core language |
| NumPy | Array operations, custom algorithm implementation |
| pandas | Data loading and inspection |
| matplotlib | Visualization |
| scikit-learn | PCA, StandardScaler, euclidean_distances, KMeans/DBSCAN (analysis only) |
| JupyterLab | Interactive notebook environment |

---

## How to Run

```bash
# 1. Clone the repository
git clone https://github.com/DaytonWickerd/Data-Mining-Projects.git
cd "Data-Mining-Projects/04-customer-segmentation-clustering"

# 2. Install dependencies
pip install -r requirements.txt

# 3. Launch JupyterLab and open the notebook
jupyter lab notebook.ipynb
```

Run all cells top to bottom (`Kernel → Restart & Run All`). Generated figures are saved to the `figures/` directory automatically.

---

## Repository Structure

```
04-customer-segmentation-clustering/
├── README.md
├── requirements.txt
├── notebook.ipynb          # Main analysis notebook
├── data/
│   └── Wholesale_customers_data.csv
└── figures/
    ├── pca_2d_projection.png
    ├── pca_cumulative_variance.png
    ├── kmeans_elbow.png
    └── kmeans_precision.png
```

---

## Notes

- K-Means and DBSCAN are implemented from scratch in Sections 2 and 3 of the notebook, without relying on `sklearn.cluster.KMeans` or `sklearn.cluster.DBSCAN` for the core algorithm logic.
- The sklearn `KMeans` and `DBSCAN` classes are used in Section 5 solely for the parameter sweep and elbow analysis, where running many configurations efficiently is the goal.
- Random seed is fixed (`np.random.seed(42)`) in the custom K-Means implementation for reproducibility.
