# Ex.No: 1B CONVERSION OF NON STATIONARY TO STATIONARY DATA
# Date: 29/04/2026

### AIM:
To perform regular differncing,seasonal adjustment and log transformatio on international airline passenger data
### ALGORITHM:
1. Import the required packages like pandas and numpy
2. Read the data using the pandas
3. Perform the data preprocessing if needed and apply regular differncing,seasonal adjustment,log transformation.
4. Plot the data according to need, before and after regular differncing,seasonal adjustment,log transformation.
5. Display the overall results.
### PROGRAM:
```
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
from statsmodels.tsa.seasonal import seasonal_decompose
df = pd.read_excel("/content/Google_Stock_Price_Test.csv.xlsx")
df["Date"] = pd.to_datetime(df["Date"])
df.set_index("Date", inplace=True)
df = df.sort_index()
stock_data = df[["Close"]].copy()
stock_data["diff"] = stock_data["Close"] - stock_data["Close"].shift(1)
result = seasonal_decompose(stock_data["Close"], model="additive", period=7)
stock_data["seasonal_resid"] = result.resid
stock_data["log"] = np.log(stock_data["Close"])
stock_data["log_diff"] = stock_data["log"] - stock_data["log"].shift(1)
result_log = seasonal_decompose(stock_data["log_diff"].dropna(), model="additive", period=7)
stock_data["log_seasonal_resid"] = result_log.resid

plt.figure(figsize=(16, 16))

plt.subplot(6, 1, 1)
plt.plot(stock_data["Close"], label="Original Close Price")
plt.legend()
plt.title("Original Google Stock Price")

plt.subplot(6, 1, 2)
plt.plot(stock_data["diff"], label="Differencing")
plt.legend()
plt.title("Regular Differencing")

plt.subplot(6, 1, 3)
plt.plot(stock_data["seasonal_resid"], label="Seasonal Residual")
plt.legend()
plt.title("Seasonal Decomposition Residual")

plt.subplot(6, 1, 4)
plt.plot(stock_data["log"], label="Log Transform")
plt.legend()
plt.title("Log Transformation")

plt.subplot(6, 1, 5)
plt.plot(stock_data["log_diff"], label="Log Differencing")
plt.legend()
plt.title("Log Differencing")

plt.subplot(6, 1, 6)
plt.plot(stock_data["log_seasonal_resid"], label="Log Seasonal Residual")
plt.legend()
plt.title("Log Seasonal Residual")

plt.tight_layout()
plt.show()

```

### OUTPUT:

Original Google Stock Price

<img width="1417" height="236" alt="image" src="https://github.com/user-attachments/assets/47654da9-46bd-4d78-8f5d-425cc7950775" />

REGULAR DIFFERENCING:

<img width="1420" height="238" alt="image" src="https://github.com/user-attachments/assets/d057b4d1-36e2-4fe4-b39c-5c3e5a43f794" />

SEASONAL ADJUSTMENT:

<img width="1421" height="240" alt="image" src="https://github.com/user-attachments/assets/bc594e1e-ec7a-47df-a659-3584413c8ba2" />

LOG TRANSFORMATION:

<img width="1413" height="242" alt="image" src="https://github.com/user-attachments/assets/b7d4161a-badb-461f-8c03-50a318fdb04a" />

Log Differencing:

<img width="1417" height="235" alt="image" src="https://github.com/user-attachments/assets/ce460aa5-72d5-4965-a018-ca072ffe12f0" />

Log Seasonal Residual:

<img width="1416" height="233" alt="image" src="https://github.com/user-attachments/assets/87ced07d-8ef3-4b64-9797-0d5f4006abb1" />

### RESULT:
Thus we have created the python code for the conversion of non stationary to stationary data on international airline passenger
data.
