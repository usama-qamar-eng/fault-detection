# Tables

## Table 1: data preparation

| Item | Value |
|---|---|
| Raw rows / raw columns | 12001 / 9 |
| Columns removed | `Unnamed: 7`, `Unnamed: 8` |
| Missing values after cleaning | 0 in every column |
| Fault rows / no-fault rows | 5496 / 6505 |
| Train / validation / test rows | 7200 / 2400 / 2401 |
| Fault fraction in train / validation / test | 0.4607 / 0.4512 / 0.4565 |

The two removed columns come from trailing commas in the CSV and hold no values at all. The label `Output (S)` was renamed to `fault`.

## Table 2: logistic regression

| Feature set | Chosen α | Final J(θ) | Validation accuracy |
|---|---|---|---|
| Set R | 1 | 0.6772 | 0.7308 |
| Set Q | 10 | 0.0534 | 0.9783 |

Training accuracy is 0.7258 for Set R and 0.9788 for Set Q.

For Set R, α = 0.01, 0.1 and 1 lower J at every iteration, while α = 10 overshoots and J jumps up and down, so we kept α = 1. For Set Q all four values lower J at every iteration, so we kept α = 10, the largest in the grid. J for Set Q is still falling slowly at iteration 2000.

## Table 3: SVM validation results

| Kernel | C | γ | Validation accuracy | Support vectors |
|---|---|---|---|---|
| linear | 0.1 | - | 0.7258 | 5849 |
| linear | 1 | - | 0.7258 | 5836 |
| linear | 10 | - | 0.7258 | 5835 |
| linear | 100 | - | 0.7258 | 5836 |
| rbf | 0.1 | 0.1 | 0.9500 | 1347 |
| rbf | 0.1 | 1 | 0.9804 | 848 |
| rbf | 1 | 0.1 | 0.9750 | 723 |
| rbf | 1 | 1 | 0.9917 | 482 |
| rbf | 10 | 0.1 | 0.9921 | 381 |
| rbf | 10 | 1 | 0.9962 | 342 |
| rbf | 100 | 0.1 | 0.9954 | 174 |
| rbf | 100 | 1 | 0.9967 | 266 |

We kept the linear SVM with C = 0.1 (all four values tie, so the first one stays) and the RBF SVM with C = 100 and γ = 1. Both are saved in `results/models/`.

## Table 4: test results

The test rows were used once, after all choices were made. The test set has 2401 rows, 1096 of them faults, and every confusion matrix adds up to 2401.

| Model | Accuracy | TN | False alarms | Missed faults | TP |
|---|---|---|---|---|---|
| Logistic regression, Set R | 0.7264 | 1305 | 0 | 657 | 439 |
| Logistic regression, Set Q | 0.9788 | 1299 | 6 | 45 | 1051 |
| Linear SVM (C=0.1) | 0.7359 | 1305 | 0 | 634 | 462 |
| RBF SVM (C=100, γ=1) | 0.9958 | 1301 | 4 | 6 | 1090 |

## Table 5: learned θ (Set Q, standardised features)

| Weight | Feature | Value |
|---|---|---|
| θ0 | intercept | 24.9209 |
| θ1 | Ia | 2.3273 |
| θ2 | Ib | -5.3581 |
| θ3 | Ic | -1.7365 |
| θ4 | Va | -0.5336 |
| θ5 | Vb | 0.4167 |
| θ6 | Vc | 0.0986 |
| θ7 | Ia² | 18.8912 |
| θ8 | Ib² | 4.7543 |
| θ9 | Ic² | 13.9569 |
| θ10 | Va² | -6.0276 |
| θ11 | Vb² | -6.4643 |
| θ12 | Vc² | -6.1407 |
