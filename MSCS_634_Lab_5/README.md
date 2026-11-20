## Purpose

In this lab, I group the Wine dataset (178 wines, 13 chemical measurements) with two methods: Hierarchical (Agglomerative) clustering and DBSCAN. I try different numbers of clusters for Hierarchical clustering and different `eps` and `min_samples` values for DBSCAN. I check the results with the Silhouette Score, Homogeneity, and Completeness (and also ARI), and I show them in scatter plots and a dendrogram.

## Results

| Method | Clusters | Noise wines | Silhouette | Homogeneity | Completeness | ARI |
|---|---|---|---|---|---|---|
| Hierarchical (Ward, 3 clusters) | 3 | 0 | 0.277 | 0.790 | 0.783 | 0.790 |
| DBSCAN (eps 2.5, min_samples 10) | 2 | 32 | 0.323 | 0.504 | 0.560 | 0.424 |

## Key insights

- Hierarchical clustering with 3 clusters was the best. It matches the 3 real wine classes well. Only 13 wines are in the wrong cluster.
- The dendrogram has a big gap between the last two merges (27.7) and the one before them (12.6). This shows 3 natural groups, and it agrees with the scores.
- DBSCAN was very sensitive to its parameters. A small eps made all wines noise. A big eps made one big cluster. Only eps 2.0 to 2.5 gave a useful result.
- The best DBSCAN found 2 clusters and 32 noise wines. It could not separate class 1 from class 0, because they are close to each other and have a similar density.
- DBSCAN has a higher silhouette (0.323), but this is not a fair comparison. The silhouette leaves out the noise points, and DBSCAN threw away 18% of the wines.

## Decisions and challenges

- I standardized the features first. Without it, `proline` (up to about 1680) would control the distances.
- I used Ward linkage for Hierarchical clustering because it makes round, compact clusters, which suits this data.
- The data has 13 features, so I used PCA to draw it in 2D. PCA keeps only 55% of the information, so the plots are a rough picture. The clusters were made with all 13 features.
- The real classes were used only to evaluate the clusters (Homogeneity, Completeness, ARI), never to make them.
- The metrics can be misleading for DBSCAN. If every wine is noise, Completeness shows 1.0, which means nothing. The silhouette ignores noise, so it can look high when most wines are thrown away. I chose the best DBSCAN setting by ARI and checked the number of noise wines.
- I used a k-distance plot and a grid of `eps` and `min_samples` values to tune DBSCAN. It took many tries to find a setting that worked.
- I used a fixed random seed (42) where randomness is used (PCA).
