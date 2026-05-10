# A5 - Data Analytics-2

✅ Tested and working as intended.

---

## Pre-requisites

- Install required libraries: `pandas`, `numpy`, `matplotlib`, `seaborn` & `scikit-learn`

```shell
pip install pandas numpy matplotlib seaborn
pip install -U scikit-learn
```

- Save the dataset [Assignment-A5-Social_Network_Ads.csv](https://git.kska.io/sppu-te-comp-content/DataScienceAndBigDataAnalytics/src/branch/main/Datasets/Assignment-A5-Social_Network_Ads.csv) in the same directory as this Jupyter notebook.

---

## Code blocks

1. Import libraries:

```python3
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
from sklearn.model_selection import train_test_split
from sklearn.preprocessing import StandardScaler
from sklearn.linear_model import LogisticRegression
from sklearn.metrics import confusion_matrix, accuracy_score, precision_score, recall_score
```

> [!TIP]
> Hit `Tab` key while typing library names (or anything else) to activate auto-complete in Jupyter notebook.

2. Load the dataset from a CSV file into a pandas DataFrame:

```python3
df= pd.read_csv("Assignment-A5-Social_Network_Ads.csv")
df.head() # Print first 5 rows
```

3. Print column names of the DataFrame:

```python3
df.columns
```

4. Convert `Gender` to numeric; Splot data (25%, 75%):

```python3
# Convert Gender to numeric
df['Gender'] = df['Gender'].map({'Male': 0, 'Female': 1})

# Features and Target
X = df[['Gender', 'Age', 'EstimatedSalary']]
y = df['Purchased']

# Split the data
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.25, random_state=42)
```

5. Feature scaling:

```python3
sc = StandardScaler()
X_train = sc.fit_transform(X_train)
X_test = sc.transform(X_test)
```

6. Train model and make predictions:

```python3
# Train the model
classifier = LogisticRegression()
classifier.fit(X_train, y_train)
# Make predictions
y_pred = classifier.predict(X_test)
```

7. Evaluate the model:

```python3
# Confusion Matrix
cm = confusion_matrix(y_test, y_pred)
print("Confusion Matrix:\n", cm)

# Extract values
TN, FP, FN, TP = cm.ravel()

# Metrics
accuracy = accuracy_score(y_test, y_pred)
error_rate = 1 - accuracy
precision = precision_score(y_test, y_pred)
recall = recall_score(y_test, y_pred)

print(f"True Positives (TP): {TP}")
print(f"False Positives (FP): {FP}")
print(f"True Negatives (TN): {TN}")
print(f"False Negatives (FN): {FN}")
print(f"Accuracy: {accuracy:.2f}")
print(f"Error Rate: {error_rate:.2f}")
print(f"Precision: {precision:.2f}")
print(f"Recall: {recall:.2f}")
```

8. Visualize:

```python3
sns.heatmap(cm, annot=True, fmt='d', cmap='Blues')
plt.xlabel("Predicted")
plt.ylabel("Actual")
plt.title("Confusion Matrix")
plt.show()
```

---

## References

1. [Jupyter notebook](https://github.com/ganimtron-10/SPPU-2019-TE-DSBDA-Lab/blob/master/Group-A/Q5.ipynb) ❌❌❌ (not referring anymore)
2. [Dataset source](https://www.kaggle.com/datasets/akram24/social-network-ads)

---
