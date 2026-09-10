<div align="center">

# 🌸 Iris Species Clustering & Dimensionality Reduction

### A Comparative Unsupervised Learning Study — K-Means, Hierarchical Clustering, DBSCAN & PCA

[![Python](https://img.shields.io/badge/Python-3.10%2B-3776AB?logo=python&logoColor=white)](https://www.python.org/)
[![scikit-learn](https://img.shields.io/badge/scikit--learn-ML-F7931E?logo=scikitlearn&logoColor=white)](https://scikit-learn.org/)
[![Pandas](https://img.shields.io/badge/Pandas-Data%20Analysis-150458?logo=pandas&logoColor=white)](https://pandas.pydata.org/)
[![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-F37626?logo=jupyter&logoColor=white)](https://jupyter.org/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

</div>

---

## 📖 Overview

In this project, I explore the classic **Iris flower dataset** through the lens of **unsupervised machine learning**. Rather than relying on the ground-truth species labels, I let three fundamentally different clustering algorithms discover the natural structure hidden in the sepal and petal measurements on their own — and then I quantitatively check afterward how closely each algorithm's discoveries line up with reality.

I benchmark **K-Means**, **Agglomerative Hierarchical Clustering**, and **DBSCAN** against each other, and use **Principal Component Analysis (PCA)** to study how dimensionality reduction affects clustering quality — evaluating every method with **Silhouette Score** and **Adjusted Rand Index (ARI)**.

## 🎯 Objectives

- [x] Perform exploratory data analysis (EDA) and standardize the features
- [x] Determine the optimal number of clusters using the Elbow Method and Silhouette Analysis
- [x] Apply K-Means clustering and visualize clusters in 2D and 3D
- [x] Reduce dimensionality with PCA and analyze explained variance
- [x] Perform Hierarchical Clustering and interpret dendrograms across three linkage strategies
- [x] Apply DBSCAN, tuning `eps` and `min_samples` via a k-distance graph and grid search
- [x] Quantitatively benchmark every algorithm with Silhouette Score and ARI
- [x] Consolidate findings into a single comparison dashboard

## 🧠 Techniques Compared

| Technique | Category | What It Does |
|---|---|---|
| **K-Means** | Centroid-based | Partitions data into *k* groups by minimizing distance to cluster centers |
| **Agglomerative Hierarchical Clustering** | Connectivity-based | Builds a tree of nested clusters from the bottom up |
| **DBSCAN** | Density-based | Groups dense regions together and flags sparse points as noise/outliers |
| **PCA** | Dimensionality reduction | Compresses 4 correlated features into 2 uncorrelated components |

## 📊 Results at a Glance

| Algorithm | Clusters | Noise Points | Silhouette | ARI vs. True Labels |
|---|---|---|---|---|
| K-Means (4D) | 3 | 0 | 0.4599 | 0.6201 |
| K-Means (PCA, 2D) | 3 | 0 | **0.5092** | 0.6201 |
| Hierarchical (Ward) | 3 | 0 | 0.4467 | 0.6153 |
| DBSCAN (eps=0.5) | 2 | 34 | 0.6559* | 0.4421 |

*\*DBSCAN's silhouette is computed only on non-noise points, so it isn't directly comparable to the others.*

**Key finding:** K-Means and Hierarchical Clustering both independently recover the true 3-species structure (ARI ≈ 0.62), and agree with each other almost as strongly as they agree with the ground truth — strong evidence the pattern is real. DBSCAN, on the other hand, merges the overlapping *versicolor*/*virginica* classes into one dense region, which is a useful illustration of where density-based clustering breaks down. Full reasoning for every result is written out in the notebook.

## 🖼️ Sample Visualizations

<table>
<tr>
<td width="50%"><img src="assets/01_eda_pairplot.png" alt="EDA Pairplot"/><p align="center"><em>Exploratory pairwise feature analysis</em></p></td>
<td width="50%"><img src="assets/02_elbow_silhouette_method.png" alt="Elbow and Silhouette Method"/><p align="center"><em>Elbow Method & Silhouette Score for optimal k</em></p></td>
</tr>
<tr>
<td width="50%"><img src="assets/03_kmeans_clusters_2d_3d.png" alt="K-Means Clusters"/><p align="center"><em>K-Means clusters — 2D & 3D views</em></p></td>
<td width="50%"><img src="assets/04_final_dashboard.png" alt="Final Dashboard"/><p align="center"><em>Final comparison dashboard — all 4 methods</em></p></td>
</tr>
</table>

## 🛠️ Tech Stack

`Python` · `NumPy` · `Pandas` · `Matplotlib` · `Seaborn` · `Scikit-learn` · `SciPy` · `Jupyter Notebook`

## 📂 Project Structure

```
Iris-Clustering-Dimensionality-Reduction/
│
├── Iris_Clustering_and_Dimensionality_Reduction_Farjana_Ferdausi.ipynb   # Main notebook
├── assets/                                                                # Exported visualizations
│   ├── 01_eda_pairplot.png
│   ├── 02_elbow_silhouette_method.png
│   ├── 03_kmeans_clusters_2d_3d.png
│   └── 04_final_dashboard.png
├── requirements.txt                                                      # Python dependencies
├── LICENSE
└── README.md
```

## 🚀 Getting Started

**1. Clone the repository**
```bash
git clone https://github.com/farjanaferdausi-cs50ai/Iris-Clustering-Dimensionality-Reduction.git
cd Iris-Clustering-Dimensionality-Reduction
```

**2. Create a virtual environment (recommended)**
```bash
python -m venv venv
source venv/bin/activate      # On Windows: venv\Scripts\activate
```

**3. Install dependencies**
```bash
pip install -r requirements.txt
```

**4. Launch the notebook**
```bash
jupyter notebook Iris_Clustering_and_Dimensionality_Reduction_Farjana_Ferdausi.ipynb
```

The dataset is loaded directly from `scikit-learn`, so no external data download is required.

## 🔍 Key Insights

1. **K-Means and Hierarchical Clustering are the most reliable algorithms for this dataset.** Both independently recover the true 3-species structure with ARI scores around 0.62, and agree with each other (ARI 0.6255) almost as strongly as they agree with the ground truth.
2. **PCA is genuinely useful here as a pre-processing step, not just for visualization.** Reducing from 4D to 2D improved the K-Means silhouette score (0.4599 → 0.5092) while the ARI stayed perfectly identical, since the first 2 principal components already capture 95.81% of total variance.
3. **DBSCAN is the wrong tool for this specific dataset — and that itself is a useful finding.** Because *versicolor* and *virginica* overlap in density rather than being separated by empty space, DBSCAN merges them into one cluster and its ARI drops to 0.4421, even while reporting a locally impressive silhouette score.
4. **The bottleneck across every algorithm is the same:** *setosa* is trivially separable by every method, while the real difficulty — and the thing that caps every algorithm's ARI around 0.6 — is the genuine biological overlap between *versicolor* and *virginica*.

## 🔮 Future Work

- Explore **Gaussian Mixture Models** for soft/probabilistic cluster boundaries
- Try **t-SNE** or **UMAP** as non-linear alternatives to PCA for visualization
- Extend the comparison framework to a higher-dimensional, real-world dataset

## 👩‍💻 About the Author

**Farjana Ferdausi**
AI/ML Engineering & Data Science | Fellow — Google Cloud Gen AI Academy APAC Edition (Cohort 3)
Agentic AI · RAG · Gemini · ADK · BigQuery MCP · Cloud Run
Former HR Professional (14+ years) at Radisson Blu Dhaka Water Garden, Bangladesh

🔗 [LinkedIn](https://www.linkedin.com/in/farjana-ferdausi/) · ✍️ [Medium](https://medium.com/@farjana.rafi1983)

## 📄 License

This project is licensed under the MIT License — see the [LICENSE](LICENSE) file for details.
