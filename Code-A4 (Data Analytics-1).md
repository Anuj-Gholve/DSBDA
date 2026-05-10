# A4 - Data Analytics-1

✅ Tested and working as intended.

---

## Pre-requisites

- Install required libraries: `pandas`, `numpy`, `seaborn`, `matplotlib` & `scikit-learn`

```shell
pip install pandas numpy seaborn matplotlib
pip install -U scikit-learn
```

- Save the dataset [Assignment-A3-BostonHousing.csv](https://git.kska.io/sppu-te-comp-content/DataScienceAndBigDataAnalytics/src/branch/main/Datasets/Assignment-A3-BostonHousing.csv) in the same directory as this Jupyter notebook.

---

## Code blocks

1. Import libraries:

```python3
import pandas as pd
import numpy as np
import seaborn as sns
import matplotlib.pyplot as plt
from sklearn.model_selection import train_test_split
from sklearn.linear_model import LinearRegression
from sklearn.metrics import mean_squared_error, r2_score
```

> [!TIP]
> Hit `Tab` key while typing library names (or anything else) to activate auto-complete in Jupyter notebook.

2. Load the dataset from a CSV file into a pandas DataFrame:

```python3
df= pd.read_csv("Assignment-A3-BostonHousing.csv")
df.head() # Prints first 5 rows
```

3. Printing information about the DataFrame:

```python3
print("Columns:\n", df.columns)
print("Info:\n", df.info())
print("Description:\n", df.describe())
```

4. Check for missing values:

```python3
print(df.isnull().sum())
```

5. Correlation matrix:

```python3
plt.figure(figsize=(12, 10))
sns.heatmap(df.corr(), annot=True, cmap='coolwarm')
plt.title("Correlation Matrix")
plt.show()
```

6. Splitting training and testing data:

```python3
X = df.drop('medv', axis=1)  # Deleted/Dropped "medv" (median value) column from dataset
y = df['medv']               # Target (Median value of owner-occupied homes)
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42) # Split data into 80% training and 20% testing
# X is independent variable; y is dependent variable
```

7. Linear regression and evaulation:

```python3
lr = LinearRegression() # Create linear regression model object "lr"
lr.fit(X_train, y_train) # Train linear regression model using "X_train" and "y_train"
y_pred = lr.predict(X_test) # Make prediction on test case (X_train); predicated value stored in variable (y_pred)

# Evaluation
print("Mean Squared Error (MSE):", mean_squared_error(y_test, y_pred))
print("R-squared (R²):", r2_score(y_test, y_pred))
```

8. Plotting graph:

```python3
plt.figure(figsize=(6,6))
plt.scatter(y_test, y_pred, color='blue')
plt.plot([min(y_test), max(y_test)], [min(y_test), max(y_test)], color='red')
plt.xlabel('Actual Prices')
plt.ylabel('Predicted Prices')
plt.title('Actual vs Predicted Prices')
plt.grid(True)
plt.show()
```

---

## References

1. [Dataset source](https://www.kaggle.com/c/boston-housing)

---
