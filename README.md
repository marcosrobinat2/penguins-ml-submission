# Palmer Penguins — PRDL and MLLB

A gradual, English-language introduction to classical machine learning. The priority is explaining what the data, fitting and evaluation mean, rather than maximising a score.

## Read and run

1. [Understanding and EDA](01_understanding_and_eda.ipynb): data source, variables, missing values, distributions and relationships in training data.
2. [Supervised learning](02_supervised_learning.ipynb): classification, regression and a small tree-depth search, with explanations, formulas and visible training code.

Download the repository files. Each notebook runs independently on CPU in Google Colab or VS Code/Jupyter. In Colab, open the notebook using the upload option and run all cells from the top; upload the original `penguins.csv` when prompted. The file stays in temporary runtime storage. No whole-Drive access is needed. In VS Code/Jupyter, place the CSV in the working directory.

The libraries are Python, pandas, NumPy, Matplotlib and scikit-learn. The notebooks print the runtime versions used. Restarting the runtime removes its variables: saved outputs do not replace running earlier cells.

## Intermediate submission — 1 November 2026

The source contains 344 observations and eight variables. A fixed 80/20 species-stratified allocation (seed 42) gives 275 development and 69 reserved final-test observations. Complete-input/response training views contain 273 rows, excluding source IDs 3 and 271 only from those views. Nine otherwise eligible rows with missing sex remain. No CSV value or recorded extreme is removed or imputed.

Classification uses four physical inputs and five saved stratified folds. Regression predicts body mass from the other three inputs and uses a separate five-fold KFold list. Both are shuffled with seed 42; any scaling is learned inside fit folds. No reserved-test eligibility, distribution or score is used for development. Prior whole-table ingestion checks are disclosed.

| Fixed method | OOF accuracy | Mean species F1 |
|---|---:|---:|
| Majority reference | 0.4432 | 0.2047 |
| Logistic regression | 0.9853 | 0.9820 |
| Depth-3 tree | 0.9231 | 0.9079 |
| Linear SVM | 0.9853 | 0.9820 |

Mean species F1 is macro-F1. Logistic and SVM give the same held-out predictions. The limited tree search compares depths 2/3/4/5 with minimum leaf size 5, selecting by mean fold macro-F1. Depths 4/5 tie at 0.9137, so 4 is selected. That selection score is not an independent estimate and does not replace the fixed-model table. GridSearchCV performs 20 sequential fits with `refit=False`; there is no final fitted selected model or test score.

| Regression method | OOF MAE (g) | OOF RMSE (g) | OOF R-squared |
|---|---:|---:|---:|
| Fit-median reference | 679.17 | 823.48 | -0.048 |
| Ordinary least squares | 325.46 | 408.10 | 0.743 |

These are development comparisons, not final-test results, universal algorithm rankings or causal findings. Large errors remain visible. Classification/regression predictors, losses, fitting procedures, metrics and the distinction between fitting and hyperparameter selection are explained in the notebook. Clustering and final testing remain outstanding for the January submission. Personal learning reflections require the author's own review.

## Reports and delivery

PRDL explains the problem, methods and results. MLLB explains the code, tools and reproduction steps. Both reports link to this repository:

https://github.com/marcosrobinat2/penguins-ml-submission

The submission includes the two executed notebooks, original CSV and guide alongside the two report PDFs. A repository link does not replace the code files required for MLLB. Reports, course material, credentials and local environments are not stored in this repository. The working Drive and Overleaf files have separate access controls.

## Data provenance and attribution

The authors' simplified `penguins` table is not a cleaning result produced by this project. Its data are distributed under CC0. We acknowledge the original collectors, Palmer Station LTER and Kristen Gorman, and the package authors Allison Marie Horst, Alison Presmanes Hill and Kristen B. Gorman.

- [Dataset documentation and licence](https://allisonhorst.github.io/palmerpenguins/).
- [Variable definitions](https://allisonhorst.github.io/palmerpenguins/reference/penguins.html).
- [CSV source](https://raw.githubusercontent.com/allisonhorst/palmerpenguins/refs/heads/main/inst/extdata/penguins.csv), acquired 23 October 2026.
- Horst, Hill and Gorman (2020), [palmerpenguins](https://doi.org/10.5281/zenodo.3960218).
- Gorman, Williams and Fraser (2014), [original ecological study](https://doi.org/10.1371/journal.pone.0090081).

CSV SHA-256: `f204db2c753b0937caac3cb35258562c14f073e4bbc76be24b4c51ce22767a93`.

The data licence does not imply a licence for all project-authored text or code. AI assistance was used for drafting and coding; the author must review, understand and explain the work. No personal learning reflection is claimed on the author's behalf.
