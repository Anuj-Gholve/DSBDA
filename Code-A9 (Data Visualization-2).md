# A9 - Data Visualization-2

✅ Tested and working as intended.

---

## Pre-requisites

- Install required libraries: `seaborn` & `matplotlib`

```shell
pip install matplotlib seaborn
```

---

## Code blocks

1. Import libraries:

```python3
import seaborn as sns
import matplotlib.pyplot as plt
from collections import Counter
```

2. Load built-in dataset:

```python3
df= sns.load_dataset('titanic')
df.head()
```

3. Describe:

```python3
# Describe
print(df.describe())
# Describe - transposed, i.e. rows and columns swapped
print(df.describe().transpose())
```

4. Mean, median, mode:  **(NOT SURE IF THIS IS NEEDED)**

```python3
# Mean, median, mode
age_data = df['age'].dropna() # Drop missing values in age & store in age_data var

sorted_age_data = sorted(age_data) # Store sorted age_data
n = len(sorted_age_data) # Store length of age_data

# Calculate mean
mean_age = sum(age_data) / len(age_data)

# Calculate median
if n % 2 == 1:  # odd
    median_age = sorted_age_data[n // 2]
else:  # even
    median_age = (sorted_age_data[n // 2 - 1] + sorted_age_data[n // 2]) / 2

# Calculate mode
age_counts = Counter(age_data)  # Count occurrences of each age
mode_age = age_counts.most_common(1)[0][0]  # Get the most common value

# Print
print(f"The mean age is: {mean_age}")
print(f"The median age is: {median_age}")
print(f"The mode age is: {mode_age}")
```

5. Boxplot:

```python
plt.figure(figsize=(8,4)) # 8 by 4 inches
sns.boxplot(x="sex", y="age", hue="survived", data= df, palette="viridis")
plt.title("Distribution of age with respect to each gender and survival Status")
plt.xlabel("Sex")
plt.ylabel("Age")
plt.show()
```

6. Violin plot:

```python3
sns.violinplot(x='sex',y='age',data=df, hue= 'survived')
```

7. Catplot:

```python3
sns.catplot(x="sex", hue="survived", data=df, kind="count")
```

---

