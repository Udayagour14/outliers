# outliers
## 1. Z-Score Method
###  A Z-score (or standard score) tells how many standard deviations a data point is from the mean.
#### formula Z = (X-𝜇)/σ
where **𝑋  is the data point, 𝜇 is the mean, and σ is the standard deviation** .
If **∣Z∣>3**, it's considered an **outlier**.
`Python Code (Z-Score)`
```python
import numpy as np
import pandas as pd
from scipy import stats

# Sample data
data = {'Value': [10, 12, 11, 13, 500, 15, 14, 13, 12, 11]}
df = pd.DataFrame(data)

# Compute Z-scores
df['Z-score'] = (df['Value'] - df['Value'].mean()) / df['Value'].std()  #Z = (X-𝜇)/σ`

# Filter outliers (Z-score > 3 or < -3)
outliers_z = df[abs(df['Z-score']) > 3] #∣Z∣>3, it's considered an **outlier**
print(outliers_z)])
```

#Another way of `Z score`
`we can apply Z score function`
```python
from scipy.stats import zscore
z_score = df.apply(zscore) #df having dataframe
outlier = (z_score.abs()>3).any(axis=1)
outlier_ = df[outlier]
print(outlier_)
```
## 2. IQR (Interquartile Range) Method
`IQR is the range between Q1 (25th percentile) and Q3 (75th percentile).`

**Formula:IQR=Q3−Q1**
`Lower bound: Q1−1.5×IQR
Upper bound: Q3+1.5×IQR`
```python
# Calculate Q1 and Q3
Q1 = df['Value'].quantile(0.25)
Q3 = df['Value'].quantile(0.75)
IQR = Q3 - Q1

# Define bounds
lower_bound = Q1 - 1.5 * IQR
upper_bound = Q3 + 1.5 * IQR

# Identify outliers
outliers_iqr = df[(df['Value'] < lower_bound) | (df['Value'] > upper_bound)]
print(outliers_iqr)
```
## 3. Visualization Methods
### a) Boxplot (Detect Outliers)
```python
import matplotlib.pyplot as plt

plt.boxplot(df['Value'])
plt.title("Boxplot for Outlier Detection")
plt.show()
```

## b) Scatter Plot with Outliers Highlighted
```python
plt.scatter(range(len(df['Value'])), df['Value'], label="Data Points")
plt.scatter(outliers_iqr.index, outliers_iqr['Value'], color='red', label="Outliers", marker='o')
plt.xlabel("Index")
plt.ylabel("Value")
plt.legend()
plt.title("Outliers in Data")
plt.show()
```
```Method	Pros	Cons
Z-score	Works well for normally distributed data	Sensitive to extreme values, not ideal for skewed data
IQR	Works well for skewed distributions	Less effective for small datasets
Boxplot	Easy to visualize	Doesn't show exact values of outliers
Scatter Plot	Clearly highlights outliers	Not useful for large datasets
```

