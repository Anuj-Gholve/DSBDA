# A10 - Data Visualization-3

✅ Tested and working as intended.

---

## Pre-requisites

- Install required libraries: `pandas`, `seaborn` & `matplotlib`

```shell
pip install pandas matplotlib seaborn
```

---

1. Import libraries:

```python3
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
```

2. Load dataset into Pandas DataFrame:

```python3
df = pd.read_csv('iris.csv')
df.head()
```

3. Features & their datatypes:

```python3
print("Feature and their types:")
df.dtypes
```

4. Histogram for each numerical feature:

```python3
plt.figure(figsize=(12, 6))

for i, column in enumerate(df.columns[:-1]):  # Exclude 'species' column
    plt.subplot(2, 2, i + 1)

    ax = plt.hist(df[column], edgecolor="black")
    plt.gca().bar_label(plt.gca().containers[0], fmt='%d')  # Add count labels
    plt.title(f"Histogram of {column}")
    plt.xlabel(column)
    plt.ylabel("Frequency")

plt.tight_layout()
plt.show()
```

5. Boxplot (for identifying outliers in this case):

```python3
plt.figure(figsize=(12, 6))
for i, column in enumerate(df.columns[:-1]):  # Exclude 'species' column
    ax = plt.subplot(2, 2, i + 1)
    # Create boxplot and store it in a container
    box_container = sns.boxplot(x=df[column], ax=ax, color='salmon')
    plt.title(f"Boxplot of {column}")

plt.tight_layout()
plt.show()
```

6. Detecting outliers:

```python3
for column in df.columns[:-1]:  # Exclude 'species' column
    Q1 = df[column].quantile(0.25)
    Q3 = df[column].quantile(0.75)
    
    IQR = Q3 - Q1
    
    lower_bound = Q1 - 1.5 * IQR
    upper_bound = Q3 + 1.5 * IQR
    
    outliers = df[(df[column] < lower_bound) | (df[column] > upper_bound)][column]

    print(f"\nFeature: {column}")
    print(f"  Mean: {df[column].mean():.2f}, Median: {df[column].median():.2f}, Std Dev: {df[column].std():.2f}")
    print(f"  Outliers Detected: {'Yes' if not outliers.empty else 'No'}","\n  " f"Outlier Values: {outliers.tolist()}" if not outliers.empty else "")
    print("-" * 40)
```

7. Violin plot:

```python3
plt.figure(figsize=(12, 8))
for i, column in enumerate(df.columns[:-1]):  # Exclude 'species' column
    plt.subplot(2, 2, i + 1)
    sns.violinplot(x=df["variety"], y=df[column], palette="Set2", hue=df['variety'])
    plt.title(f"Violin Plot of {column} by variety")

plt.tight_layout()
plt.show()
```

---

## References

- [Dataset source-1](https://archive.ics.uci.edu/ml/machine-learning-databases/iris/iris.data) *(not exactly, but yes, kinda)*
- [Dataset source-2](https://archive.ics.uci.edu/dataset/53/iris) *(not exactly, but yes, kinda)*

---