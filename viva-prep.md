# DSBDA Archive: Problem-Statement Cross-Check and Theory Notes

This document maps each notebook (`a1.ipynb`–`a10.ipynb`) to the Savitribai Phule Pune University (TY Computer Engineering) problem statements, states whether every required operation is present, notes gaps or bugs, and explains the **ideas**, **libraries**, and **keywords** you can use in a viva or report.

**Datasets in this folder (3):** `Iris.csv`, `BostonHousing.csv`, `Social_Network_Ads.csv`  
**Note:** Several notebooks call `pd.read_csv("iris.csv")`. The file on disk is `Iris.csv`. On Windows the name is often case-insensitive, but on Linux/macOS you should rename the file or change the path to match exactly.

---

## Quick summary table

| # | Notebook | PS topic | All PS steps covered? | Main gaps / fixes |
|---|----------|----------|---------------------|-------------------|
| 1 | `a1.ipynb` | Data Wrangling I | **Mostly** | No explicit written **data source URL/description** in the notebook; use `Iris.csv` vs `iris.csv` on strict OS |
| 2 | `a2.ipynb` | Data Wrangling II | **Partially** | `fillna(...)` **not assigned** back to `df` (missing `df['col'] = ...` or `inplace=True`); no explicit **textual documentation** of transformation rationale; **inconsistencies** (e.g. 500/450 marks) handled only indirectly via outliers |
| 3 | `a3.ipynb` | Descriptive statistics | **Yes** | Syllabus typo repeats “versicolor”; your code correctly uses **virginica** too |
| 4 | `a4.ipynb` | Data Analytics I (Linear regression) | **Yes** | Optional: mention **train/test split ratio** and **feature names** in theory |
| 5 | `a5.ipynb` | Data Analytics II (Logistic regression) | **Mostly** | **Bug:** last print says “Recall” but prints **`precision`** again |
| 6 | `a6.ipynb` | Data Analytics III (Naïve Bayes) | **Mostly** | Multi-class iris: single **TP/TN/FP/FN** is ambiguous; you use **macro** precision/recall (good) but do not print four scalars as in binary PS wording |
| 7 | `a7.ipynb` | Text analytics | **Yes** | `nltk.download("all")` is slow/heavy; POS on sample differs from full pipeline order |
| 8 | `a8.ipynb` | Data Visualization I | **Yes** | One plot title says “based on **age**” but the plot is **sex**—cosmetic fix |
| 9 | `a9.ipynb` | Data Visualization II | **Partially** | PS asks for **written observations**; notebook has plot but **no observation text** |
| 10 | `a10.ipynb` | Data Visualization III | **Mostly** | Outlier block only reflects the **last** column in the loop unless you print **per feature**; typo “dectected” |

---

## 1. Data Wrangling I — `a1.ipynb`

### Cross-check vs PS

| Step | Required | Present in code? |
|------|----------|------------------|
| Import libraries | Yes | `pandas`, `sklearn.preprocessing` (`LabelEncoder`, `MinMaxScaler`) |
| Describe data + source URL | Yes | **Weak:** Iris is implied; **add** a markdown cell: UCI / Kaggle URL and column meanings |
| Load into DataFrame | Yes | `pd.read_csv("iris.csv")` |
| Preprocessing: missing values | Yes | `df.isnull().sum()` |
| `describe()`, variable types, dimensions | Yes | `df.describe()`, `df.info()`, `df.shape` |
| Summarize / fix dtypes | Yes | `df.dtypes`, `astype('category')` for `Species` |
| Normalization | Yes | `MinMaxScaler` on numeric flower measurements |
| Categorical → quantitative | Yes | `LabelEncoder` on `Species` |

### What the code is doing (theory)

- **`import pandas as pd`:** `pandas` gives **DataFrame** (2D table) and **Series** (1D column); `pd` is a conventional alias.
- **`pd.read_csv(...)`:** Reads a comma-separated text file into a **DataFrame** (rows = samples, columns = variables).
- **`df.head()`:** Shows the first rows for a quick sanity check.
- **`df.isnull().sum()`:** `isnull()` marks missing cells; **`.sum()`** counts `True` per column (missing count).
- **`df.describe()`:** For numeric columns, returns **count, mean, std, min, quartiles, max** — first numerical “feel” of the data.
- **`df.info()`:** Non-null counts and **dtypes** (`int64`, `float64`, `object`, etc.).
- **`df.shape`:** Tuple `(rows, columns)` — **dimensions**.
- **`astype('category')`:** Stores repeated strings efficiently and marks the column as **categorical** (finite set of levels).
- **`MinMaxScaler`:** Maps each numeric feature to **[0, 1]** using \((x - \min) / (\max - \min)\) per column after **fit** on training data (here, the whole frame).
- **`LabelEncoder`:** Maps each category string to an **integer** (0, 1, 2, …). This turns **nominal** labels into numbers for some algorithms (note: some models treat integers as ordered; **one-hot encoding** is often safer for nominal data).

---

## 2. Data Wrangling II — `a2.ipynb`

### Cross-check vs PS

| Step | Required | Present in code? |
|------|----------|------------------|
| Academic performance dataset | Yes | Synthetic dict → `pd.DataFrame` |
| Missing values | Yes | `isnull().sum()` |
| Handle missing | **Bug risk** | Lines like `df['Maths'].fillna(...)` **do not modify** `df` unless you assign: `df['Maths'] = df['Maths'].fillna(...)` or `fillna(..., inplace=True)` |
| Inconsistencies | Partial | Extreme marks (500, 450) act as **outliers**; no separate rule-based “inconsistency” fix |
| Outliers on numeric | Yes | **IQR rule**: \(Q1 - 1.5 \times IQR\), \(Q3 + 1.5 \times IQR\); outside → **median** |
| Transformation + reason | Partial | `MinMaxScaler` on **Attendance** → **scale change** for interpretation; **add** markdown: why min–max (bounded 0–1, comparable to other scaled features) |
| Histogram | Extra | `plt.hist` on Attendance — not required by PS but fine |

### Theory keywords

- **`np.nan`:** IEEE floating “Not a Number” — pandas uses it for **missing** numeric cells.
- **`fillna`:** Replaces missing values (mean/median/mode/constant). **Must assign** result to persist.
- **IQR (Interquartile Range):** \(Q3 - Q1\); robust spread measure; **1.5×IQR** fences are standard for boxplot-style outlier flags.
- **`np.where(condition, x, y)`:** Vectorized “if condition then x else y” for arrays/Series.
- **`MinMaxScaler`:** Here used to put **Attendance** on **[0, 1]** for easier comparison or downstream models.

---

## 3. Descriptive statistics — `a3.ipynb`

### Cross-check vs PS

| Step | Required | Present in code? |
|------|----------|------------------|
| Summary stats by categorical group | Yes | `groupby('Species').agg({...: ['mean','median','min','max','std']})` |
| List of numeric values per category | Yes | Dictionary `species_group` → list of `SepalLengthCm` per species |
| Iris species stats (setosa, versicolor, virginica) | Yes | Loop + `describe()` per species (syllabus duplicates “versicolor”; third species is **virginica**) |

### Theory keywords

- **`groupby('Species')`:** Splits the DataFrame into **groups** — one per species — then aggregate functions run **within** each group.
- **`.agg({...})`:** **Aggregation**: multiple functions per column in one call.
- **Mean / median / std:** **Central tendency** (mean, median) and **spread** (std); **min/max** show range.
- **`describe()`:** Default percentile table (including **25%, 50%, 75%**) for numeric columns in each subset.

---

## 4. Data Analytics I — Linear regression — `a4.ipynb`

### Cross-check vs PS

| Step | Required | Present in code? |
|------|----------|------------------|
| Boston Housing, predict price | Yes | Target `medv`; features = other columns |
| Linear regression | Yes | `sklearn.linear_model.LinearRegression` |
| Train/test + evaluation | Yes | `train_test_split`, `mean_squared_error`, `r2_score` |
| Optional visualization | Yes | Scatter actual vs predicted + diagonal line |

### Theory keywords

- **Linear regression:** Models target \(y\) as a **linear combination** of features: \(y \approx w_1 x_1 + \cdots + w_p x_p + b\).
- **`train_test_split`:** Holds out a **test** set to estimate **generalization** (not memorizing training rows).
- **MSE:** Average squared error — penalizes large errors heavily.
- **\(R^2\):** Fraction of variance in \(y\) explained by the model (1 is best on training-like scale; can be negative on test).

---

## 5. Data Analytics II — Logistic regression — `a5.ipynb`

### Cross-check vs PS

| Step | Required | Present in code? |
|------|----------|------------------|
| Logistic regression on `Social_Network_Ads.csv` | Yes | |
| Confusion matrix + TP, FP, TN, FN | Yes | `confusion_matrix`; unpack with `ravel()` |
| Accuracy, error rate, precision, recall | **Mostly** | **Print bug:** recall line uses **`precision`** variable |

### Theory keywords

- **Logistic regression:** Models **probability of class 1** with the **logistic (sigmoid)** function of a linear score — used for **binary classification**.
- **`StandardScaler`:** Z-score features \((x - \mu) / \sigma\) so gradient-based solvers behave well.
- **Confusion matrix (binary):** Rows ≈ **actual**, columns ≈ **predicted** (sklearn default). **TN, FP, FN, TP** counts.
- **Accuracy:** \((TP + TN) / (TP + TN + FP + FN)\).
- **Error rate:** \(1 - \text{Accuracy}\).
- **Precision:** \(TP / (TP + FP)\) — “of predicted positives, how many correct?”
- **Recall:** \(TP / (TP + FN)\) — “of actual positives, how many found?”

---

## 6. Data Analytics III — Naïve Bayes — `a6.ipynb`

### Cross-check vs PS

| Step | Required | Present in code? |
|------|----------|------------------|
| Naïve Bayes on iris | Yes | `GaussianNB` |
| Confusion matrix | Yes | Heatmap + printed `cm` |
| Accuracy, error, precision, recall | Yes | Uses **`average='macro'`** (fair for 3 classes) |

### Theory keywords

- **Naïve Bayes:** Applies **Bayes’ theorem** with a “naïve” assumption: features are **conditionally independent** given the class. **GaussianNB** assumes each feature is **normally distributed** within each class.
- **Multi-class metrics:** One **confusion matrix** is \(3 \times 3\). **Macro** precision/recall averages metrics **per class** (unweighted), treating classes equally.

### PS wording note

For **multi-class**, “single TP, FP, TN, FN” is not unique; examiners often accept **per-class** breakdown or **macro/micro** averages — **state this** in your oral explanation.

---

## 7. Text analytics — `a7.ipynb`

### Cross-check vs PS

| Step | Required | Present in code? |
|------|----------|------------------|
| Sample document | Yes | Long `text` string |
| Tokenization | Yes | `sent_tokenize`, `word_tokenize` |
| POS tagging | Yes | `nltk.pos_tag` |
| Stop word removal | Yes | `stopwords.words('english')` + filter loop |
| Stemming | Yes | `PorterStemmer` |
| Lemmatization | Yes | `WordNetLemmatizer` |
| TF-IDF representation | Yes | `TfidfVectorizer` + `fit_transform` |

### Theory keywords

- **Tokenization:** Splitting text into **sentences** or **words** (tokens).
- **POS tagging:** Assigning **part-of-speech** (NN, VB, …) using a tagger model.
- **Stop words:** High-frequency words (the, is, …) often removed to focus on **content words**.
- **Stemming:** Crude **suffix chopping** to a stem (fast, not always a real word).
- **Lemmatization:** Dictionary-based **lemma** (canonical form); better meaning, needs **WordNet** data.
- **TF (term frequency):** How often a term appears in a document (normalized variants exist).
- **IDF (inverse document frequency):** Down-weights terms that appear in **many** documents; highlights **discriminative** words.
- **`TfidfVectorizer`:** Builds a **sparse matrix** of TF-IDF weights for a **corpus** (here, one document still gets a vector).

---

## 8. Data Visualization I — `a8.ipynb`

### Cross-check vs PS

| Step | Required | Present in code? |
|------|----------|------------------|
| Seaborn `titanic` | Yes | `sns.load_dataset('titanic')` |
| Patterns with Seaborn | Yes | `countplot` for survival, sex×survival, class×survival |
| Histogram of `fare` | Yes | `sns.histplot(df['fare'], ...)` |

### Theory keywords

- **`countplot`:** Bar counts of **categorical** frequencies; **`hue`** splits bars by a second category (e.g. survived).
- **`histplot`:** **Histogram** — distribution of a numeric variable (`fare`) in bins; **`kde=True`** adds a smooth density curve.

---

## 9. Data Visualization II — `a9.ipynb`

### Cross-check vs PS

| Step | Required | Present in code? |
|------|----------|------------------|
| Box plot: age vs sex, by survived | Yes | `sns.boxplot(x='sex', y='age', hue='survived', data=df)` |
| Written observations | **Missing** | Add bullet observations (e.g. median age by group, whisker spread, outliers) |

### What to write for observations (example lines you can adapt)

- Compare **median** age lines for male vs female for `survived=0` vs `1`.
- Note **whisker length** and **outliers** (dots) for each subset.
- Relate to historical context (e.g. “women and children first” — often higher survival among younger/female groups in aggregate plots).

---

## 10. Data Visualization III — `a10.ipynb`

### Cross-check vs PS

| Step | Required | Present in code? |
|------|----------|------------------|
| Load Iris into DataFrame | Yes | `pd.read_csv("iris.csv")` |
| List features and types | Yes | `df.dtypes` |
| Histogram per feature | Yes | Loop + `sns.histplot` on numeric columns (excluding `Id` / handling columns carefully) |
| Boxplot per feature | Yes | Loop + `sns.boxplot` |
| Compare distributions / outliers | **Weak** | Outlier detection loop should **print per column** (or concatenate results); currently easy to only show **last** column’s outliers |

### Theory keywords

- **Histogram vs boxplot:** Histogram shows **overall shape** (modality, skew); boxplot shows **quartiles, median, IQR**, and **outlier** points beyond fences.
- **Outlier rule (1.5×IQR):** Same idea as in Wrangling II.

---

## Choosing “any one” for tomorrow — practical tips

1. **Pick the notebook whose outputs already run cleanly** on your laptop (especially `a7` if NLTK data is downloaded).
2. For **oral explanation**, prepare **one sentence each** for: *data → method → metric → plot → limitation*.
3. **Fix the small bugs** (`a2` fillna assignment, `a5` recall print, `a9` observations, `a10` per-column outliers) so live demo matches the PS literally.

---

## Glossary of common sklearn / pandas symbols

| Symbol / API | Meaning |
|--------------|--------|
| `X`, `y` | Features matrix / target vector |
| `fit` | Learn parameters from data (means for scaler, weights for model) |
| `transform` | Apply learned parameters to data |
| `fit_transform` | Fit on training slice, then transform same slice |
| `predict` | Output labels (classifier) or numbers (regressor) |
| `random_state` | Fixes RNG seed for **reproducible** splits |

---

*Generated for the archive at `archive (1)` containing `a1.ipynb`–`a10.ipynb` and the three CSV datasets.*
