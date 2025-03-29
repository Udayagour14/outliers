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
```
from scipy.stats import zscore
z_score = df.apply(zscore) #df having dataframe
outlier = (z_score.abs()>3).any(axis=1)
outlier_ = df[outlier]
print(outlier_)




