# Palmer Penguins — PRDL and MLLB

One didactic machine-learning study: data understanding, species classification, mass regression and descriptive clustering. The priority is understanding what each algorithm learns and how its predictions are evaluated.

## Notebooks

1. [Understanding and EDA](01_understanding_and_eda.ipynb): all variables, data quality, distributions, correlations and Simpson's paradox.
2. [Supervised learning](02_supervised_learning.ipynb): shared methodology; logistic regression, decision tree, linear SVM, KNN and Random Forest; joint assessment; regression; reserved-test evaluation and uncertainty.
3. [Unsupervised learning](03_unsupervised_learning.ipynb): scaling, PCA and K-means on development measurements, without species in fitting.

Every notebook runs independently on CPU in Colab or VS Code/Jupyter. Place the unchanged penguins.csv in the working directory, or upload it when Colab prompts. Run from the top after each kernel restart. Packages: pandas, NumPy, Matplotlib, scikit-learn and SciPy. Saved outputs do not recreate variables.

## Common evaluation methodology

The source has 344 rows and eight columns. The original species-stratified split (seed 42) gives 275 development and 69 reserved-test observations. Complete-measurement development views use 273 rows; source IDs 3 and 271 are excluded from those views only. Missing sex alone excludes no row. No CSV value or recorded extreme is changed.

All five classifier families use the same five outer stratified folds and three inner stratified folds for setting selection. Scaling remains inside pipelines. The majority reference uses the same outer held-out rows. Each family is selected, fitted and assessed under this protocol.

| Classifier family | Mean outer-fold macro-F1 |
|---|---:|
| Logistic regression | 0.9812 |
| Decision tree | 0.9052 |
| Linear SVM | 0.9815 |
| KNN | 0.9812 |
| Random Forest | 0.9483 |

Mean fold F1 differs from pooled OOF F1; both are labelled in the notebook. The small differences between logistic regression, SVM and KNN do not establish significant superiority. Development exploration and selecting a family from its outer score limit independence. The selection rule was fixed before test access; a three-fold development search selected C=10 for linear SVM, followed by refitting on eligible development rows.

Regression compares a fit-median reference with untuned OLS using three inputs (mass is removed from predictors) and a separate five-fold KFold list. Development OOF OLS MAE is 325.46 g versus 679.17 g for the median reference.

## Reserved-test assessment and descriptive profiles

All 69 reserved observations meet the required-variable rules. Selected SVM accuracy is 68/69 (98.55%), macro-F1 0.9829; the majority reference is 30/69. The SVM Wilson 95% accuracy interval is 92.24–99.74%. One predeclared exact McNemar comparison against the majority reference gives 39/1 discordant pairs, p=7.46e-11; this does not compare the leading measurement-based classifiers.

OLS test MAE is 276.83 g, RMSE 348.58 g and R-squared 0.803, versus median-reference MAE 644.57 g. A 5,000-resample paired row bootstrap gives a conditional percentile 95% OLS-MAE interval of 228.37–326.65 g and an MAE-reduction interval of 249.68–484.87 g. Intervals use working sampling assumptions, do not model the entire stratified collection design and do not include refitting uncertainty. No test-based model revision is performed.

Two PCA components retain 88.57% of standardised development variance. K-means fits all four scaled measurements: three teaching groups, not a claimed optimal k, with sizes 108/98/67 and silhouette 0.459. Species is used for the inherited allocation and later interpretation, never for fitted scaler/PCA/clustering or choosing their settings.

## Explanation and delivery

The five classifiers have sibling model sections in notebook 02 and both reports. A common fitting loop exposes selection, fit and held-out prediction. First-outer-round fitted models are inspected without extra fits: logistic coefficients/softmax, tree/Gini rules, SVM support observations, KNN neighbours and forest bootstrap/probability averaging. Reports explain scientific interpretation (PRDL) and code/reproduction (MLLB).

The package contains three executed notebooks, the original CSV, this guide and two report PDFs. Reports and teaching materials are outside this public repository. Personal learning reflections must be written by the author. No university-platform submission is made automatically.

## Data provenance and attribution

The authors' simplified `penguins` table is not a cleaning result produced by this project. Its data are distributed under CC0. We acknowledge the original collectors, Palmer Station LTER and Kristen Gorman, and the package authors Allison Marie Horst, Alison Presmanes Hill and Kristen B. Gorman.

- [Dataset documentation and licence](https://allisonhorst.github.io/palmerpenguins/).
- [Variable definitions](https://allisonhorst.github.io/palmerpenguins/reference/penguins.html).
- [CSV source](https://raw.githubusercontent.com/allisonhorst/palmerpenguins/refs/heads/main/inst/extdata/penguins.csv), acquired 23 October 2026.
- Horst, Hill and Gorman (2020), [palmerpenguins](https://doi.org/10.5281/zenodo.3960218).
- Gorman, Williams and Fraser (2014), [original ecological study](https://doi.org/10.1371/journal.pone.0090081).

CSV SHA-256: `f204db2c753b0937caac3cb35258562c14f073e4bbc76be24b4c51ce22767a93`.

The data licence does not imply a licence for all project-authored text or code. AI assistance was used for drafting and coding; the author must review, understand and explain the work. No personal learning reflection is claimed on the author's behalf.
