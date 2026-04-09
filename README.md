# Data Mining Projects

A collection of data mining and machine learning projects completed for CSCI 347. Each project applies core data science techniques to real-world datasets.

---

## Projects

### [Heart Disease EDA](./01-heart-disease-eda/)
**Topics:** Exploratory Data Analysis, Statistical Analysis, Feature Engineering

Analyzes the UCI Heart Disease dataset (Cleveland subset, 303 patients) to identify physiological indicators of heart disease severity. Covers data cleaning, mean imputation, covariance and correlation analysis, and scatter plot visualization across a 0–4 severity scale. All statistical functions implemented from scratch.

[View Project →](./01-heart-disease-eda/README.md)

---

### [Congressional Twitter Network Analysis](./02-congress-network-analysis/)
**Topics:** Graph Theory, Social Network Analysis, Centrality Measures, Degree Distribution

Analyzes the Congressional Twitter Network (475 Congress members, 13,289 directed weighted edges) alongside the Facebook social graph (4,039 nodes). Implements 12 graph algorithms from scratch — including betweenness, closeness, eigenvector centrality, and clustering coefficient — then applies NetworkX for full-scale centrality rankings, PageRank, and power-law degree distribution analysis.

[View Project →](./02-congress-network-analysis/README.md)

---

### [PCA, Dimensionality Reduction & Clustering](./03-pca-dimensionality-reduction/)
**Topics:** PCA, Dimensionality Reduction, K-Means, DBSCAN, Variance Analysis

Applies PCA and clustering to synthetic and real-world data across five sections. Manually interprets covariance, decorrelation, and variance explained before using sklearn. Shows that 7 of 13 Boston Housing features capture 90% of variance, compares k-means vs DBSCAN cluster geometry on PCA-projected data, and visualizes DBSCAN geographic clusters on the California Housing dataset.

[View Project →](./03-pca-dimensionality-reduction/README.md)

---

## Tech Stack

- Python 3, Jupyter Notebooks
- pandas, NumPy, Matplotlib
- NetworkX, scikit-learn
