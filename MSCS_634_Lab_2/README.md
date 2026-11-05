## Purpose

In this lab, I compare two models, KNN and Radius Neighbors (RNN), on the Wine dataset. It has 178 wines, 13 chemical measurements for each, and 3 wine types. I check how the choice of k and radius changes accuracy.


## Results

KNN accuracy
- k=1: 0.778
- k=5, 11, 15, 21: 0.806

RNN accuracy
- radius 350: 0.722
- radius 400, 450, 500: 0.694
- radius 550, 600: 0.667

## Key insights

- KNN did a little better when k went from 1 to 5. With k=1, one odd neighbor can give a wrong answer. After k=5, accuracy stayed the same.
- RNN did worse as the radius got bigger. A big radius pulls in wines from other types, so the vote gets mixed up.
- KNN was better than RNN every time (best 0.806 vs 0.722).
- The features have very different sizes. Proline goes up to about 1680, while most others are small, so proline controls the distance. When I scaled the features, KNN reached 0.972 to 1.000.
- KNN is a safer first choice because it always has k neighbors to vote. RNN is useful when a fixed distance has a real meaning and the data is spread evenly.

## Decisions and challenges

- I did not scale the features for the main results, because the radius values in the lab (350 to 600) only fit the raw data. I added one extra scaled check for KNN.
- RNN gives an error if a test point has no neighbors inside the radius. I told it to use the most common class in that case. This never happened, so it did not change the results.
- The test set is small (36 wines), so one wine is about 2.8% accuracy. I did not read too much into small differences.
