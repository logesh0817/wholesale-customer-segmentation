# Wholesale Customer Segmentation

An unsupervised learning project that groups wholesale customers by their annual spending patterns using several clustering techniques.

## Dataset

- **File:** `Wholesale_Data.csv` (440 customers)
- **Features used:** `Fresh`, `Milk`, `Grocery`, `Frozen`, `Detergents_Paper`, `Delicassen` (annual spend per product category)
- **Dropped before clustering:** `Channel` and `Region`

## Techniques

- **K-Means:** elbow method to choose k, then a 6-cluster model that adds a `segment` label per customer
- **Hierarchical clustering:** Agglomerative clustering with a Ward-linkage dendrogram
- **DBSCAN:** density-based clustering that also identifies noise points
- **PCA:** reduces the data to 2 components to visualise the K-Means clusters

## Results

**K-Means (k = 6, chosen with the elbow method)** produced these segments:

| Segment | Customers | Profile |
|---|---|---|
| 1 | 241 | Low spend across all categories (the typical small customer) |
| 2 | 107 | Mainly Fresh (average about 23,600) |
| 3 | 74 | Mainly Milk, Grocery and Detergents_Paper |
| 0 | 11 | Very high Fresh spend (average about 60,400) |
| 4 | 5 | Very high Milk, Grocery and Detergents_Paper |
| 5 | 2 | Very high Frozen and Delicatessen |

**Other techniques**

- **Hierarchical clustering (2 clusters):** split the customers into 306 and 134.
- **PCA (2 components):** kept about **86.5%** of the variance, so the 2D plot is a good summary of the data.
- **DBSCAN (`eps=0.9`, `min_samples=15`):** found 0 clusters and labelled all 440 customers as noise. The spend values are in the thousands and the data is unscaled, so `eps=0.9` is far too small.

**What I learned**

- Most customers are small buyers (segment 1), while a few large buyers (segments 0, 4 and 5) behave almost like outliers.
- Customers can be separated by what they buy: fresh-focused, and milk/grocery/detergent-focused.
- Next steps: scale the features with `StandardScaler` before clustering, and re-tune DBSCAN afterwards.

## Getting started

```bash
pip install numpy pandas matplotlib scipy scikit-learn jupyter
jupyter notebook unsup.ipynb
```

## Files

| File | Description |
|---|---|
| `unsup.ipynb` | Full notebook: clustering and visualisation |
| `Wholesale_Data.csv` | Wholesale customer dataset |
