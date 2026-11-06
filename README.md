# Rice variety classification

Can seven measurements of a rice grain distinguish Cammeo from Osmancik? I compared seven classifiers on 3,810 grains and tested how two preprocessing choices affected their predictions. Logistic regression on the original measurements achieved the highest accuracy, correctly classifying **701 of 762 grains (91.99%)**.

[Explore the notebook, model comparisons and confusion matrices](rice_classification.ipynb)

## What changed the predictions?

Standardising the features raised k-nearest neighbours accuracy from 86.48% to 90.94% and SVM accuracy from 86.88% to 91.08%. Both models use distances between observations, which depend on the units of the measurements.

Grain area and convex area had a Pearson correlation of 0.9989 in the training data. I removed convex area and reran the two models with the lowest macro F1 after scaling. The same change had opposite effects.

| Model | Errors with 7 features | Errors with 6 features | Macro F1 before | Macro F1 after |
|---|---:|---:|---:|---:|
| Gaussian Naive Bayes | 80 | 76 | 0.8919 | 0.8975 |
| Decision tree | 78 | 82 | 0.8953 | 0.8899 |

## Evaluation

I used a stratified 80/20 split with seed 42 (3,048 training grains and 762 test grains) and fitted the scaler on the training rows. Each classifier used the same split. The notebook reports accuracy, macro precision, macro recall, macro F1 and ROC-AUC for both rounds.

I used the test-set ranking to choose the two models for the feature-removal experiment. The four-error differences are exploratory results on this split. A fresh holdout would help assess whether they generalise.

## Run locally

From the project directory, use Python 3.12 in a fresh environment and run:

```shell
python -m pip install -r requirements.txt
python -m jupyterlab rice_classification.ipynb
```

Choose **Run → Run All Cells**. The dataset is included alongside the notebook.

## Data and citation

İlkay Çınar and Murat Köklü (2019). *Rice (Cammeo and Osmancik)*. UCI Machine Learning Repository. The original ARFF file is distributed here unchanged under [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/). [Dataset DOI](https://doi.org/10.24432/C5MW4Z).

Çınar, İ. and Köklü, M. (2019). Classification of Rice Varieties Using Artificial Intelligence Methods. *International Journal of Intelligent Systems and Applications in Engineering*, 7(3), 188–194. [Paper DOI](https://doi.org/10.18201/ijisae.2019355381).
