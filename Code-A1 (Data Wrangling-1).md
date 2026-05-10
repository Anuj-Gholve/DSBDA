# A1 - Data Wrangling-1

✅ Tested and working as intended.

---

## Pre-requisites

- Install required libraries: `pandas` & `numpy`

```shell
pip install pandas numpy
```

- Save the dataset [iris.csv](https://git.kska.io/sppu-te-comp-content/DataScienceAndBigDataAnalytics/src/branch/main/Datasets/iris.csv) in the same directory as this Jupyter notebook.

---

## Code blocks

1. Import libraries:

```python3
import pandas as pd
import numpy as np
```

2. Load the dataset from a CSV file into a pandas DataFrame:

```python3
df=pd.read_csv('iris.csv')
df.describe() # Print description of DataFrame
```

3. Print first and last 5 values:

```python3
print("First 5 values:\n", df.head())
print ("Last 5 values:\n", df.tail())
```

4. Print duplicated values:

```python3
df.duplicated()
```

5. Print null values true/false:

```python3
df.isnull()
```

6. Print summary of DataFrame:

```python3
df.info()
```

7. Print shape, i.e. rows + columns:

```python3
df.shape
```

8. Print null (true/false) values in `sepal.length` column:

```python3
df["sepal.length"].isnull()
```

9. Delete/Drop `petal.length` column:

```python3
y = df.drop(["petal.length"], axis=1) # axis=1 column. For row, axis=0
print(y)
```

10. In `variety` column, replace `Setosa` with `0` and `Virginica` with `1`:

```python3
df['variety'].replace(['Setosa', 'Virginica'], [0,1], inplace=True)
print(df)
```

11. Print sum of NULL values in each column:

```python3
df.isnull().sum()
```

---
