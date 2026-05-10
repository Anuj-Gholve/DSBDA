# A6 - Data Analytics-3

✅ Tested and working as intended.

---

## Pre-requisites

- Install required libraries: `pandas`, `numpy`, `matplotlib`, `seaborn` & `scikit-learn`

```shell
pip install pandas numpy matplotlib seaborn
pip install -U scikit-learn
```

- Save the dataset [iris.csv](https://git.kska.io/sppu-te-comp-content/DataScienceAndBigDataAnalytics/src/branch/main/Datasets/iris.csv) in the same directory as this Jupyter notebook.

---

## Code blocks

1. Import libraries:

```python3
import pandas as pd
import numpy as np
import seaborn as sns
import matplotlib.pyplot as plt
from sklearn.model_selection import train_test_split
from sklearn.preprocessing import StandardScaler
from sklearn.naive_bayes import GaussianNB
from sklearn.metrics import confusion_matrix, accuracy_score, precision_score, recall_score
```

2. Load the dataset from a CSV file into a Pandas DataFrame:

```python3
df = pd.read_csv("iris.csv")
df.head()
```

3. Set independent & dependent variables; Train, test, split:

```python3
# Set independent and dependent variables
X = df.drop('variety', axis=1) # Independent variable
y = df['variety'] # Dependent variable

# train test split
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)
```

4. Scale features:

```python3
scaler = StandardScaler()
X_train_scaled = scaler.fit_transform(X_train)
X_test_scaled = scaler.transform(X_test)
```

5. Train Naive Bayes model:

```python3
# Train Naive Bayes model
model = GaussianNB()
model.fit(X_train_scaled, y_train)

# Predict
y_pred = model.predict(X_test_scaled)
```

6. Evaulate the model; Plot Confusion Matrix:

```python3
# Evaluate the model
cm = confusion_matrix(y_test, y_pred, labels=model.classes_)
cm_df = pd.DataFrame(cm, index=model.classes_, columns=model.classes_)

# Plot Confusion Matrix
sns.heatmap(cm_df, annot=True, cmap='Blues', fmt='d')
plt.title('Confusion Matrix')
plt.xlabel('Predicted')
plt.ylabel('Actual')
plt.show()
```

7. Set variables for accuracy, precision, recall & error rate + print em:

```python3
accuracy = accuracy_score(y_test, y_pred)
precision = precision_score(y_test, y_pred, average='macro')
recall = recall_score(y_test, y_pred, average='macro')
error_rate = 1 - accuracy

print(f"Accuracy: {accuracy:.2f}")
print(f"Error Rate: {error_rate:.2f}")
print(f"Precision (Macro): {precision:.2f}")
print(f"Recall (Macro): {recall:.2f}")
```

---