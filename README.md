# Msc-Project
High-Dimensional Clustering & ISOLET Case Studies (Display-Only Notebooks)

This project investigates clustering in high dimensions and a real-world speech dataset (ISOLET). All notebooks are **display-only**: they render tables/plots inline and **do not save** files. We compare classic algorithms (KMeans, Agglomerative/Ward, GMM, DBSCAN), study robustness to outliers/noise/features, and evaluate on ISOLET with fair, unsupervised preprocessing.

## Project Overview

### Datasets
- **Simulated Gaussian blobs (high-D)**  
  Synthetic datasets with controllable cluster separation, outliers, variance, PCA projections, and extra noise features.
- **ISOLET (UCI id=54)**  
  7,797 spoken letters, 617 features. We standardize, apply PCA, and evaluate clustering vs. true A–Z classes.

### Experiments
- **Exp1 — Outliers:** vary outlier proportion; evaluate ARI/CH/DBI (silhouette skipped here by design).
- **Exp2 — Cluster StdDev:** increase within-cluster std; also plot metrics vs. min Mahalanobis separation.
- **Exp3 — PCA Dimensions:** project to k ∈ {2, 10, 50, 100}; assess metric trends with dimension.
- **Exp4 — Added Noise Features:** append pure noise features; test robustness.
- **Exp5 — Matched-k (RAW vs PCA→k\*):** compare data generated at intrinsic k\* to PCA-reduced base data at the same k\*.
- **ISOLET Case Study (final, clean):**  
  PCA=50 (variance printed), KMeans elbow (~11) **reported**, and **evaluation at k=26** to match the 26 letter classes; DBSCAN eps via k-distance knee (percentile fallback); summary table (ARI, Silhouette, ExecTime_s, DBSCAN clusters/noise); elbow plot; **ARI vs cumulative explained variance** (legend right, no grid); **Hungarian-mapped confusion heatmap** with % and counts.
- **ISOLET — PCA vs t-SNE (visuals only):** unsupervised PCA/t-SNE embeddings; labels used strictly for coloring.
- **Manual vs scikit-learn KMeans:** same initialization, iterations, and data for a fair head-to-head.

### Methods
- **Clustering:** KMeans, Agglomerative (Ward), Gaussian Mixture (full covariance), DBSCAN.  
  Also **GMM(BIC)** for model-selection diagnostics (excluded from comparison lines but reported in tables).
- **Metrics:** Adjusted Rand Index (ARI, on inliers), Silhouette (non-noise), Calinski–Harabasz (CH), Davies–Bouldin (DBI), and **ExecTime_s**.
- **Statistics:** Bootstrap CIs (ARI), paired Wilcoxon tests with Benjamini–Hochberg FDR across algorithms/conditions.
- **Preprocessing:** Standardization; PCA for dimensionality control (and PCA-50 in ISOLET).  
  **t-SNE** is used **only** for visualization; never as a preprocessing step for clustering.

### Evaluation Policy (ISOLET)
- **Unsupervised fitting:** Labels are **never** used to fit or tune models.  
- **k=26 is evaluation-only:** We **report** the KMeans elbow (~11), but to fairly assess recovery of the 26 letter classes we **run KMeans/Agglomerative/GMM with k=26** **only for evaluation**. Metrics (e.g., ARI) and the confusion heatmap use true labels **post-hoc**.  
- **DBSCAN:** eps chosen by k-distance knee (with percentile fallback); number of clusters is emergent and may include noise.

## Data Source & Citation

This case study uses the **ISOLET** dataset from the UCI Machine Learning Repository.

Cole, R., & Fanty, M. (1991). *ISOLET*. UCI Machine Learning Repository. https://doi.org/10.24432/C51G69

We access ISOLET via `ucimlrepo` and use labels **only** for evaluation/visualization (e.g., ARI, confusion heatmap).
