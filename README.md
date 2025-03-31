# Stock Market Data Analysis

## Overview
This project provides an interactive Python script for analyzing stock market data using Pandas, Seaborn, and Matplotlib. It includes features for data cleaning, exploratory data analysis (EDA), and visualization of stock price trends.


# Stock-Market-Data-Analysis
Project to display us of Python on Data Visualization and Analysis
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
from datetime import datetime

# Load the Excel file
file_path = r"C:\Users\jayni\Desktop\Important Links\stock_market_data.xlsx"

## Features
- Reads stock market data from an Excel file.
- Cleans and preprocesses data, including handling missing values and date conversions.
- Computes daily and monthly percentage changes in stock prices.
- Supports user-defined date range filtering.
- Offers multiple visualization types:
  1. Barchart
  2. Histogram
  3. Pie Chart
  4. Line Plot
  5. Line Graph
  6. Seaborn Boxplot
  7. Matplotlib Plot
  8. Area Plot
  9. Scatter Plot
- Provides interactive input for customized analysis.

## Prerequisites
Ensure you have the following Python libraries installed:
```bash
pip install pandas matplotlib seaborn openpyxl
```

## Usage
1. Place your stock market data file (`stock_market_data.xlsx`) in the project directory.
2. Run the script:
   ```bash
   python stock_analysis.py
   ```
3. Enter the start and end dates when prompted.
4. Choose a visualization type by entering a number (1-9).
5. View the generated charts and insights.

## Example Output
### Monthly Change Calculation:
```
Month-wise percentage change:
Stock Symbol  Year-Month
AAPL          2022-02     0.03
              2022-03    -0.01
GOOGL         2022-02    -0.02
              2022-03     0.04
...
```
### Visualization Example:
- Selecting option `3` generates a **Pie Chart** displaying the **market share of top 5 stocks**.

## Error Handling
- Handles invalid date inputs.
- Prevents crashes due to missing or incorrect data.

## Contributing
Feel free to contribute by improving the analysis or adding new visualization types!

## License
This project is licensed under the MIT License.

