## Purpose

In this lab, I group the Wine dataset into 3 clusters with two methods, K-Means and K-Medoids. The dataset has 178 wines and 13 chemical measurements. I check the clusters with the Silhouette Score and the Adjusted Rand Index (ARI), and I plot them side by side.



## Results

K-Means
- Silhouette: 0.285
- ARI: 0.897

K-Medoids
- Silhouette: 0.268
- ARI: 0.741

## Key insights

- K-Means was better on both scores. The silhouette gap is small, but the ARI gap is big.
- Both silhouette scores are low, so the clusters are not far apart. They overlap a bit.
- K-Means matched the real wine classes well. Only 6 wines were in the wrong cluster. K-Medoids put 15 wines from class 1 in the class 0 cluster.
- Both methods find three groups in about the same places. They differ at the border between class 0 and class 1.
- K-Means is a good choice for clean, scaled, round-shaped data. K-Medoids is better when there are outliers, or when you want each cluster center to be a real data point.

## Decisions and challenges

- I standardized the features with z-score first. Without it, proline (up to about 1680) would control the distances.
- scikit-learn has no K-Medoids. scikit-learn-extra would not work with the newer numpy here (binary error), so I used the kmedoids package (FasterPAM) with Euclidean distance.
- The data has 13 features, so I used PCA to draw it in 2D. PCA keeps only 55% of the variance, so the plots are a rough picture. The clusters were made with all 13 features.
- I used a fixed random seed (42) so the results can be repeated. Results from one run should not be over-read.
