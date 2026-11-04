# Palmer Penguins — PRDL and MLLB

A small, didactic classical machine-learning project. The priority is understanding data, fitting, hyperparameter selection and evaluation.

## Read and run

1. [Understanding and EDA](01_understanding_and_eda.ipynb): variables, data quality, distributions, correlations and Simpson's paradox.
2. [Supervised learning](02_supervised_learning.ipynb): initial fixed models, regression, KNN and Random Forest with formulas, settings and worked prediction inspections, nested validation, final test and uncertainty.
3. [Unsupervised learning](03_unsupervised_learning.ipynb): standardisation, PCA and K-means; species is excluded from the unsupervised fit and added for interpretation; the inherited split was stratified by species.

Each notebook runs independently on CPU in Colab or VS Code/Jupyter. Download the files. In Colab upload a notebook, run from the top and upload the unchanged penguins.csv when prompted. In Jupyter place the CSV in the working directory. Libraries: pandas, NumPy, Matplotlib, scikit-learn and SciPy. Runtime versions are printed. Saved outputs do not recreate variables after a restart.

## Verified ML study — reviewed 4 November 2026

The unchanged source has 344 observations and eight columns. A fixed species-stratified 80/20 split, seed 42, gives 275 development and 69 test observations. Complete-measurement development views use 273 rows; source rows 3 and 271 are excluded from those views only. Missing sex excludes no otherwise usable row. No values or extremes are changed.

Initial fixed comparisons and a limited depth search remain labelled development exercises. The extension uses five outer stratified folds and three inner stratified folds to select settings inside assessment. All scaling stays in pipelines. Small fixed searches compare logistic regression, linear SVM, a decision tree, KNN and a 100-tree Random Forest. Regression compares a median reference and untuned OLS using a separate five-fold KFold list.

| Procedure | Mean external-fold macro-F1 |
|---|---:|
| Logistic regression | 0.9812 |
| Linear SVM | 0.9815 |
| Decision tree | 0.9052 |
| KNN | 0.9812 |
| Random Forest | 0.9483 |

Small differences do not show superiority among leading families. The pre-test rule selected linear SVM by highest mean external-fold F1; a three-fold development search then chose C=10. Development was already explored; nested CV does not erase that history. Test rows never enter fitting or selection.

All 69 test rows meet the eligibility rule. Final SVM accuracy is 68/69 (98.55%), macro-F1 0.9829; the majority reference is 30/69 (43.48%). The SVM Wilson 95% accuracy interval is 92.24–99.74%. A single pre-specified exact McNemar comparison against the majority reference uses 39/1 discordant pairs, p=7.46e-11. This does not compare SVM against logistic/KNN or test equal macro-F1.

OLS test MAE is 276.83 g, RMSE 348.58 g and R-squared 0.803, versus median-reference MAE 644.57 g. A 5,000-resample paired row bootstrap, seed 42, gives a percentile 95% OLS-MAE interval of 228.37–326.65 g and a reference-minus-OLS MAE interval of 249.68–484.87 g. These approximate intervals condition on fitted models and assume sufficiently independent observations. No post-test tuning was performed.

PCA retains 88.57% of scaled development variance in two components. K-means fits all four scaled inputs without labels: three teaching groups (not an optimal k claim), seed 42, ten initialisations. Group sizes are 108, 98 and 67; silhouette is 0.459. These are descriptive quantities, not prediction accuracy.

## Understanding KNN and Random Forest

Section 31 of notebook 02 explains both methods, what fit stores or learns, their hyperparameters, scaling, limits and the distinction between fitting and selection. Section 32.1 traces a held-out KNN query through fitted scaling, four-input distances, neighbour labels and class proportions. Section 32.2 inspects bootstrap samples and verifies that the mean probability vector of all 100 trees equals RandomForestClassifier.predict_proba. Scikit-learn averages probabilities; this need not equal hard-label majority voting. These inspections reuse outer-round-1 fitted estimators and perform no additional fits. The existing searches, metrics and final selection are unchanged.

## Coherence and reproducibility review

All three notebooks were re-executed independently on 4 November 2026. Split IDs agree across notebooks. Independent calculations verify confusion/F1 arithmetic, first-fold logistic softmax probabilities, NumPy OLS, Wilson and paired-test arithmetic, PCA variance ratios, K-means inertia and silhouette. Earlier pending-work statements have been corrected. Initial fixed comparisons, nested development assessment and final-test scores are distinct. The uncertainty intervals are working approximations conditional on fitted models and do not model the full species-stratified collection design. Personal reflection remains for the author.

## Reports and delivery

PRDL develops formulation and interpretation; MLLB explains code and reproduction. Both link to this public repository. The delivery package includes three executed notebooks, original CSV, this guide and two PDFs. Reports, teaching materials, environments and credentials remain outside GitHub. Personal learning reflections must be written by the author; no university submission has been made automatically.

## Data provenance and attribution

The authors' simplified `penguins` table is not a cleaning result produced by this project. Its data are distributed under CC0. We acknowledge the original collectors, Palmer Station LTER and Kristen Gorman, and the package authors Allison Marie Horst, Alison Presmanes Hill and Kristen B. Gorman.

- [Dataset documentation and licence](https://allisonhorst.github.io/palmerpenguins/).
- [Variable definitions](https://allisonhorst.github.io/palmerpenguins/reference/penguins.html).
- [CSV source](https://raw.githubusercontent.com/allisonhorst/palmerpenguins/refs/heads/main/inst/extdata/penguins.csv), acquired 23 October 2026.
- Horst, Hill and Gorman (2020), [palmerpenguins](https://doi.org/10.5281/zenodo.3960218).
- Gorman, Williams and Fraser (2014), [original ecological study](https://doi.org/10.1371/journal.pone.0090081).

CSV SHA-256: `f204db2c753b0937caac3cb35258562c14f073e4bbc76be24b4c51ce22767a93`.

The data licence does not imply a licence for all project-authored text or code. AI assistance was used for drafting and coding; the author must review, understand and explain the work. No personal learning reflection is claimed on the author's behalf.
