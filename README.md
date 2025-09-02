# Ex.No: 03   COMPUTE THE AUTO FUNCTION(ACF)
## Date: 2.09.25

### AIM:
To Compute the AutoCorrelation Function (ACF) of the data for the first 35 lags to determine the model
type to fit the data.
### ALGORITHM:
1. Import the necessary packages
2. Find the mean, variance and then implement normalization for the data.
3. Implement the correlation using necessary logic and obtain the results
4. Store the results in an array
5. Represent the result in graphical representation as given below.
### PROGRAM:
```
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt

df = pd.read_csv("usedcars.csv")

# Show first few rows to identify numeric columns
print(df.head())
print("\nNumeric columns available:\n", df.select_dtypes(include=[np.number]).columns)

df['Mileage'] = (
    df['Mileage']
    .astype(str)                 # make sure all are strings
    .str.replace(",", "")        # remove commas
    .str.extract(r'(\d+\.?\d*)') # extract numeric part
    .astype(float)               # convert to float
)

data = df['Mileage'].dropna().values
N = len(data)
lags = range(35)
autocorr_values = []

mean_data = np.mean(data)
variance_data = np.var(data)

for lag in lags:
    if lag == 0:
        autocorr_values.append(1)
    else:
        auto_cov = np.sum((data[:-lag] - mean_data) * (data[lag:] - mean_data)) / N
        autocorr_values.append(auto_cov / variance_data)

plt.figure(figsize=(10, 6))
plt.stem(lags, autocorr_values, use_line_collection=True)
plt.title('Autocorrelation of Used Cars Data (Mileage)')
plt.xlabel('Lag')
plt.ylabel('Autocorrelation')
plt.grid(True)
plt.show()
```

### OUTPUT:

<img width="1003" height="641" alt="Screenshot 2025-09-02 091947" src="https://github.com/user-attachments/assets/880ff820-8e21-4c3d-8e00-3252f9fb6670" />


### RESULT:
        Thus we have successfully implemented the auto correlation function in python.
