# Ex.No: 03   COMPUTE THE AUTO FUNCTION(ACF)
Date: 25/05/26

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
import matplotlib.pyplot as plt

import numpy as np

data = [3, 16, 156, 47, 246, 176, 233, 140, 130,
101, 166, 201, 200, 116, 118, 247,
209, 52, 153, 232, 128, 27, 192, 168, 208,
187, 228, 86, 30, 151, 18, 254,
76, 112, 67, 244, 179, 150, 89, 49, 83, 147, 90,
33, 6, 158, 80, 35, 186, 127]

lags = range(35)


```python
import matplotlib.pyplot as plt
import numpy as np
import pandas as pd

# Load the dataset
file_path = "student_performance.csv"

# Read CSV file
df = pd.read_csv(file_path)

# Display dataset columns
print("Columns in Dataset:")
print(df.columns)

# Select numeric columns only
numeric_columns = df.select_dtypes(include=[np.number])

# Check if dataset has numeric columns
if numeric_columns.shape[1] == 0:
    print("No numeric columns found.")
else:
    # Select first numeric column
    column_name = numeric_columns.columns[0]
    
    # Remove missing values
    data = numeric_columns[column_name].dropna().values

    print("\nSelected Column:", column_name)

    # Data length
    N = len(data)

    # Maximum lag
    max_lag = min(35, N - 1)

    # Mean and variance
    mean_data = np.mean(data)
    variance_data = np.var(data)

    # Store autocorrelation values
    autocorr_values = []

    # Calculate autocorrelation
    for lag in range(max_lag + 1):

        if lag == 0:
            autocorr_values.append(1)

        else:
            numerator = np.sum(
                (data[:-lag] - mean_data) *
                (data[lag:] - mean_data)
            ) / N

            autocorrelation = numerator / variance_data

            autocorr_values.append(autocorrelation)

    # Plot graph
    plt.figure(figsize=(10, 6))

    plt.stem(range(max_lag + 1), autocorr_values)

    plt.title(f'Autocorrelation Plot of {column_name}')

    plt.xlabel('Lag')

    plt.ylabel('Autocorrelation')

    plt.grid(True)

    plt.show()

```
    
    

### OUTPUT:
<img width="754" height="644" alt="image" src="https://github.com/user-attachments/assets/99e8387f-f46a-42d5-9519-3449e292a4c4" />

### RESULT:
        Thus we have successfully implemented the auto correlation function in python.
