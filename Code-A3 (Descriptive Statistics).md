# A3 - Descriptive Statistics

✅ Tested and working as intended.

---

## Pre-requisites

- Install required libraries: `pandas`

```shell
pip install pandas
```

---

## Code blocks

### Problem Statement - Part 1 (data.csv)

1. Import library

```python3
import pandas as pd
```

2. Generate data and load into DataFrame:

```python3
# Generate data
data = {
    'age': [25, 30, 22, 40, 55, 60, 33, 28, 45, 50],
    'income': [50000, 60000, 45000, 70000, 80000, 90000, 65000, 62000, 75000, 85000],
    'age_group': ['20-30', '30-40', '20-30', '40-50', '50-60', '50-60', '30-40', '20-30', '40-50', '50-60']
}

# Define data in DataFrame
df = pd.DataFrame(data)
```

3. Group data by `age_group`, compute statistics for `income` + print:

```python3
# Group the data by age_group and compute summary statistics for 'income'
summary_stats = df.groupby('age_group')['income'].describe()

# Print summary
print(summary_stats)
```

4. Group the data by `age_group`; Select `income` column for each of the groups created; Calculate median for `income`:

```python3
# Group the data by age_group; Select income column for each of the groups created; Calculate median for income
median_income = df.groupby('age_group')['income'].median()

# Print dat median
print("Median Income by Age Group:")
print(median_income)
```

5. Print column names:

```python3
print("Column Names:", df.columns)
```

6. Modified dataset with repeated values; define in DataFrame:

```python3
# Modified dataset with repeated values
data = {
    'age': [25, 30, 25, 40, 55, 60, 33, 28, 45, 50, 25, 30, 28, 30, 25],
    'income': [50000, 60000, 50000, 70000, 80000, 90000, 65000, 62000, 75000, 85000, 50000, 60000, 62000, 70000, 75000],
    'age_group': ['20-30', '30-40', '20-30', '40-50', '50-60', '50-60', '30-40', '20-30', '40-50', '50-60', '20-30', '30-40', '20-30', '30-40', '20-30']
}

# Define data in DataFrame
df = pd.DataFrame(data)
```

7. Calculate mode:

```python3
# Calculate the mode for each column
mode_age = df['age'].mode()
mode_income = df['income'].mode()
print(f"Mode of Age: {mode_age.values}")
print(f"Mode of Income: {mode_income.values}")
```

---

### Problem Statement - Part 2 (iris.csv)

- Save the dataset [iris.csv](https://git.kska.io/sppu-te-comp-content/DataScienceAndBigDataAnalytics/src/branch/main/Datasets/iris.csv) in the same directory as this Jupyter notebook.

1. Load dataset and print first 5 rows:

```python3
# Load iris.csv in the DataFrame
df = pd.read_csv('iris.csv')

print(df.head()) # Print first 5 columns
```

2. Group data; Compute percentiles; Display:

```python3
# Group the data by species and display summary statistics
summary_stats_species = df.groupby('variety').describe()

# Compute specific percentiles and statistics
percentiles = df.groupby('variety').quantile([0.25, 0.5, 0.75])

# Display summary statistics and percentiles
summary_stats_species = df.groupby('variety').describe()

print("\nPercentiles by Species:")
print(percentiles)
```

3. Group the data by variety; Select sepal.width column for each of the groups created; Display summary statistics:

```python3
# Group the data by variety; Select sepal.width column for each of the groups created; Display summary statistics
summary_stats_species = df.groupby('variety')['sepal.width'].describe()

print("\nSummary Statistics by Species for Sepal Width:")
print(summary_stats_species)
```

4. Group by variety and compute the median for numeric columns:

```python3
# Group by variety and compute the median for numeric columns
median_values = df.groupby('variety').median()

print("Median Values by Species:")
print(median_values)
```

5. Group the data by variety; Select sepal.width column for each of the groups created; Display median:

```python3
# Group the data by variety; Select sepal.width column for each of the groups created; Display median
median_sepal_length = df.groupby('variety')['sepal.length'].median()
print("Median Sepal Length by Species:")
print(median_sepal_length)
```

6. Calculate & print mode for sepal.width:

```python3
# Calculate & print mode for sepal.width
mode_width = df['sepal.width'].mode()
print(f"Mode of Width: {mode_width.values}")
```

---
