# DSBDA Viva Preparation Notes (Enhanced Version)

This document explains all the DSBDA practicals (`a1.ipynb` to `a10.ipynb`) in a much more descriptive and viva-friendly way. Along with checking whether the problem statement requirements are completed, this file also explains:

- What each code block is doing
- Why specific libraries/functions are used
- Important theory concepts
- Common viva questions
- Practical tips for explanation during external viva
- Small bugs/improvements in the notebooks

These notes are designed to help you explain your practicals confidently during demonstrations and viva.

---

# Dataset Information

Datasets used in this folder:

1. `Iris.csv`
2. `BostonHousing.csv`
3. `Social_Network_Ads.csv`

### Important Note
Some notebooks use:

```python
pd.read_csv("iris.csv")
```

But the actual file name is:

```python
Iris.csv
```

Windows usually ignores case sensitivity, but Linux/macOS do not.
So if the file does not load, rename the dataset or correct the file path.

---

# Quick Summary Table

| No. | Notebook | Topic | Status | Important Notes |
|----|----|----|----|----|
| 1 | a1.ipynb | Data Wrangling I | Mostly Complete | Add dataset source description |
| 2 | a2.ipynb | Data Wrangling II | Partially Complete | `fillna()` not assigned properly |
| 3 | a3.ipynb | Descriptive Statistics | Complete | Good implementation |
| 4 | a4.ipynb | Linear Regression | Complete | Add theory explanation |
| 5 | a5.ipynb | Logistic Regression | Mostly Complete | Recall print bug |
| 6 | a6.ipynb | Naive Bayes | Mostly Complete | Multi-class TP/TN explanation needed |
| 7 | a7.ipynb | Text Analytics | Complete | `nltk.download("all")` is heavy |
| 8 | a8.ipynb | Visualization I | Complete | Minor title correction |
| 9 | a9.ipynb | Visualization II | Partial | Add written observations |
| 10 | a10.ipynb | Visualization III | Mostly Complete | Outlier logic improvement needed |

---

# 1. Data Wrangling I — `a1.ipynb`

## Objective
Perform preprocessing operations on an open-source dataset.

The practical mainly focuses on:

- Loading dataset
- Checking missing values
- Understanding data types
- Normalization
- Converting categorical data into numeric form

---

## Libraries Used

```python
import pandas as pd
from sklearn.preprocessing import LabelEncoder, MinMaxScaler
```

### Explanation

### `pandas`
Used for handling datasets in table format.
It provides:

- DataFrame
- Series
- Data cleaning tools
- Statistical operations

### `LabelEncoder`
Used to convert text categories into numbers.

Example:

| Species | Encoded |
|---|---|
| Setosa | 0 |
| Versicolor | 1 |
| Virginica | 2 |

### `MinMaxScaler`
Used for normalization.
It converts values between 0 and 1.

Formula:

\[
X_{scaled} = \frac{X - X_{min}}{X_{max} - X_{min}}
\]

This helps algorithms treat all features equally.

---

## Important Functions

### `pd.read_csv()`
Reads CSV file and converts it into a DataFrame.

### `df.head()`
Shows first 5 rows.
Useful for quick verification.

### `df.info()`
Displays:

- Number of rows
- Column names
- Non-null values
- Data types

### `df.describe()`
Generates statistical summary:

- Mean
- Standard deviation
- Minimum
- Maximum
- Quartiles

### `df.shape`
Returns:

```python
(rows, columns)
```

### `df.isnull().sum()`
Checks missing values in each column.

---

## Viva Questions

### Q1. Why normalization is required?
Normalization prevents large-valued features from dominating small-valued features.

### Q2. Difference between Label Encoding and One-Hot Encoding?

| Label Encoding | One-Hot Encoding |
|---|---|
| Converts category into integer | Creates separate binary columns |
| May create false ordering | No ordering problem |

### Q3. What is a DataFrame?
A 2-dimensional tabular structure provided by pandas.

---

# 2. Data Wrangling II — `a2.ipynb`

## Objective
Handle missing values, outliers, inconsistencies, and perform transformations.

---

## Important Concepts

### Missing Values
Missing values are empty cells in the dataset.

Example:

```python
NaN
```

### Handling Missing Values

```python
df['Maths'] = df['Maths'].fillna(df['Maths'].mean())
```

Important:

```python
df['Maths'].fillna(...)
```

alone does NOT modify the original DataFrame.
You must assign it back.

---

## Outlier Detection

Outliers are abnormal/extreme values.

Example:

```python
500
```

marks in a dataset where normal marks are around 50–100.

### IQR Method

Formula:

\[
IQR = Q3 - Q1
\]

Outlier conditions:

\[
Value < Q1 - 1.5 \times IQR
\]

or

\[
Value > Q3 + 1.5 \times IQR
\]

---

## Histogram Explanation

```python
plt.hist(df['Attendance'], bins=5)
```

### What Histogram Shows
A histogram shows distribution of data.

- X-axis → attendance values
- Y-axis → frequency/count

Taller bars mean more students fall in that range.

---

## Viva Questions

### Q1. What is IQR?
Interquartile Range measures spread of middle 50% data.

### Q2. Why use median for outlier replacement?
Median is less affected by extreme values.

### Q3. Difference between mean and median?

| Mean | Median |
|---|---|
| Average | Middle value |
| Affected by outliers | Robust to outliers |

---

# 3. Descriptive Statistics — `a3.ipynb`

## Objective
Calculate statistical measures for different categories.

---

## Main Operations

### `groupby()`
Splits data into groups.

Example:

```python
df.groupby('Species')
```

Creates separate groups for:

- Setosa
- Versicolor
- Virginica

---

## Statistical Measures

| Measure | Meaning |
|---|---|
| Mean | Average |
| Median | Middle value |
| Std | Spread of data |
| Min | Smallest value |
| Max | Largest value |

---

## Why Standard Deviation is Important?

Small standard deviation:

- Data points are close to mean

Large standard deviation:

- Data points are spread out

---

## Viva Questions

### Q1. What is descriptive statistics?
It summarizes and describes important features of data.

### Q2. What does groupby do?
It creates groups based on category values.

---

# 4. Linear Regression — `a4.ipynb`

## Objective
Predict house prices using Boston Housing dataset.

---

## What is Linear Regression?

Linear regression finds relationship between:

- Independent variables (features)
- Dependent variable (target)

Equation:

genui{"math_block_widget_always_prefetch_v2":{"content":"y = mx + c"}}

Where:

- `m` = slope
- `c` = intercept
- `y` = predicted value

---

## Important Functions

### `train_test_split()`
Splits dataset into:

- Training data
- Testing data

Training data teaches the model.
Testing data checks performance.

---

## Evaluation Metrics

### Mean Squared Error (MSE)

Measures average squared prediction error.

Formula:

genui{"math_block_widget_always_prefetch_v2":{"content":"MSE = \frac{1}{n}\sum (y_i - \hat{y}_i)^2"}}

Smaller MSE is better.

---

### R² Score

Measures how well the model explains variance.

Range:

- 1 → perfect
- 0 → poor
- negative → very poor

---

## Viva Questions

### Q1. Difference between regression and classification?

| Regression | Classification |
|---|---|
| Predicts continuous value | Predicts category |
| Example: price | Example: spam/not spam |

### Q2. What is overfitting?
When model memorizes training data and performs poorly on new data.

---

# 5. Logistic Regression — `a5.ipynb`

## Objective
Perform binary classification using Logistic Regression.

---

## Logistic Regression

Used when output is categorical.

Example:

- Purchased / Not Purchased
- Spam / Not Spam

---

## Sigmoid Function

Converts output into probability.

genui{"math_block_widget_always_prefetch_v2":{"content":"\sigma(x)=\frac{1}{1+e^{-x}}"}}

Output range:

```python
0 to 1
```

---

## Confusion Matrix

| | Predicted Yes | Predicted No |
|---|---|---|
| Actual Yes | TP | FN |
| Actual No | FP | TN |

---

## Metrics

### Accuracy

genui{"math_block_widget_always_prefetch_v2":{"content":"Accuracy = \frac{TP + TN}{TP + TN + FP + FN}"}}

### Precision

genui{"math_block_widget_always_prefetch_v2":{"content":"Precision = \frac{TP}{TP + FP}"}}

### Recall

genui{"math_block_widget_always_prefetch_v2":{"content":"Recall = \frac{TP}{TP + FN}"}}

---

## Important Bug

Last print statement prints precision again instead of recall.

Fix:

```python
print("Recall:", recall)
```

---

# 6. Naive Bayes — `a6.ipynb`

## Objective
Classify Iris dataset using Naive Bayes.

---

## Bayes Theorem

genui{"math_block_widget_always_prefetch_v2":{"content":"P(A|B)=\frac{P(B|A)P(A)}{P(B)}"}}

---

## Why Called “Naive”?

Because algorithm assumes all features are independent.

Example:

- Petal length
- Petal width

are treated independently.

---

## Gaussian Naive Bayes

Assumes data follows normal distribution.

Bell-shaped curve assumption.

---

## Viva Questions

### Q1. Advantage of Naive Bayes?
Fast and works well for text classification.

### Q2. Limitation?
Independence assumption is often unrealistic.

---

# 7. Text Analytics — `a7.ipynb`

## Objective
Perform NLP preprocessing.

---

## NLP Pipeline

1. Tokenization
2. Stopword Removal
3. Stemming
4. Lemmatization
5. TF-IDF

---

## Tokenization

Breaks text into words/sentences.

Example:

```python
"I love AI"
```

becomes:

```python
['I', 'love', 'AI']
```

---

## Stemming vs Lemmatization

| Stemming | Lemmatization |
|---|---|
| Removes suffix | Uses dictionary meaning |
| Faster | More accurate |
| Example: studying → studi | studying → study |

---

## TF-IDF

### TF
Measures frequency of term.

### IDF
Reduces importance of common words.

Important words get higher score.

---

## Viva Questions

### Q1. Why remove stopwords?
To reduce unnecessary words and noise.

### Q2. Why use TF-IDF?
To identify important words in document.

---

# 8. Data Visualization I — `a8.ipynb`

## Objective
Visualize Titanic dataset using Seaborn.

---

## Seaborn

Python library for statistical visualization.
Built on top of matplotlib.

---

## Count Plot

Shows count of categorical values.

Example:

```python
sns.countplot(x='survived', data=df)
```

---

## Histogram

Shows distribution of continuous values.

Example:

```python
sns.histplot(df['fare'])
```

---

## Viva Questions

### Q1. Difference between matplotlib and seaborn?

| Matplotlib | Seaborn |
|---|---|
| Basic plotting | Statistical plotting |
| More coding | Simpler and attractive |

---

# 9. Data Visualization II — `a9.ipynb`

## Objective
Create boxplots and analyze distributions.

---

## Boxplot Components

| Part | Meaning |
|---|---|
| Middle line | Median |
| Box | IQR |
| Whiskers | Spread |
| Dots | Outliers |

---

## Example Observations

- Female passengers had higher survival rates.
- Younger passengers survived more often.
- Some extreme age outliers are visible.

---

## Viva Questions

### Q1. Why use boxplot?
To detect spread and outliers.

### Q2. What are whiskers?
They represent data spread excluding outliers.

---

# 10. Data Visualization III — `a10.ipynb`

## Objective
Study feature distributions and detect outliers.

---

## Histograms

Used to understand:

- Symmetry
- Skewness
- Data concentration

---

## Boxplots

Useful for:

- Outlier detection
- Median comparison
- Spread analysis

---

## Important Improvement

Outlier detection should print results for each feature separately.

Otherwise only last feature output may appear.

---

# Common Viva Questions for All Practicals

## Q1. Why preprocessing is important?
Real-world data contains missing values, noise, and inconsistencies.
Preprocessing improves model performance.

---

## Q2. Difference between supervised and unsupervised learning?

| Supervised | Unsupervised |
|---|---|
| Has labels | No labels |
| Example: classification | Example: clustering |

---

## Q3. What is machine learning?
A technique where systems learn patterns from data and make predictions.

---

## Q4. Difference between training and testing data?

| Training Data | Testing Data |
|---|---|
| Used to train model | Used to evaluate model |

---

## Q5. Why visualization is important?
Visualization helps understand patterns, trends, and anomalies easily.

---

# Final Practical Tips

1. Always explain:

```text
Input → Processing → Output
```

2. Mention why specific algorithms are used.

3. Explain graphs properly:

- X-axis
- Y-axis
- Trend
- Observation

4. During viva:

- Speak slowly
- Explain logic step-by-step
- Mention practical applications

5. Common external question:

```text
"Why did you choose this algorithm?"
```

Prepare one reason for each algorithm.

---

# Simple Algorithm Selection Guide

| Algorithm | Used For |
|---|---|
| Linear Regression | Predict continuous values |
| Logistic Regression | Binary classification |
| Naive Bayes | Probabilistic classification |
| TF-IDF | Text feature extraction |
| MinMaxScaler | Normalization |
| LabelEncoder | Convert text to numbers |

---

# Final Conclusion

These practicals cover the complete DSBDA workflow:

- Data preprocessing
- Statistical analysis
- Machine learning
- NLP
- Visualization

Understanding the logic behind functions is more important than memorizing code.

During viva, focus on:

- Why the step is performed
- What output it generates
- How it improves analysis

That approach will help you answer confidently even if the external changes questions slightly.

