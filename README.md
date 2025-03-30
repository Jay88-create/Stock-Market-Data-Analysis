# Stock-Market-Data-Analysis
Project to display us of Python on Data Visualization and Analysis
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
from datetime import datetime

# Load the Excel file
file_path = r"C:\Users\jayni\Desktop\Important Links\stock_market_data.xlsx"

def analyze_stock_data():
    df = pd.read_excel(file_path, sheet_name="Sheet1")
    
    # Convert 'Date' column to datetime format
    df['Date'] = pd.to_datetime(df['Date'])
    
    while True:
        # Ask user for date range
        start_date = input("Enter the start date (YYYY-MM-DD): ")
        end_date = input("Enter the end date (YYYY-MM-DD): ")
        
        # Convert user input to datetime
        df_filtered = df[(df['Date'] >= start_date) & (df['Date'] <= end_date)]
        
        # Calculate daily returns
        df_filtered["Daily Return"] = df_filtered.groupby("Stock Symbol")["Close"].pct_change()
        
        # Select top 5 stocks based on highest average closing price
        top_stocks = df_filtered.groupby("Stock Symbol")["Close"].mean().nlargest(5).index
        df_selected = df_filtered[df_filtered["Stock Symbol"].isin(top_stocks)]
        
        # Ask user for visualization type
        print("Choose a visualization type: bar, histogram, line graph, scatterplot, heatmap")
        vis_type = input("Enter visualization type: ").strip().lower()
        
        # Generate visualization
        plt.figure(figsize=(12, 6))
        
        if vis_type == "bar":
            df_selected.groupby("Stock Symbol")["Close"].mean().plot(kind='bar', color='blue')
            plt.title("Average Closing Price of Top 5 Stocks")
            plt.ylabel("Price")
        
        elif vis_type == "histogram":
            sns.histplot(df_selected, x="Close", hue="Stock Symbol", bins=20, kde=True)
            plt.title("Histogram of Closing Prices")
        
        elif vis_type == "line graph":
            for stock in top_stocks:
                stock_data = df_selected[df_selected["Stock Symbol"] == stock]
                plt.plot(stock_data["Date"], stock_data["Close"], label=stock)
            plt.xlabel("Date")
            plt.ylabel("Price")
            plt.title("Stock Prices Over Time")
        
        elif vis_type == "scatterplot":
            sns.scatterplot(data=df_selected, x="Date", y="Close", hue="Stock Symbol")
            plt.xticks(rotation=45)
            plt.title("Stock Prices Scatterplot")
        
        elif vis_type == "heatmap":
            pivot_table = df_selected.pivot(index="Date", columns="Stock Symbol", values="Close")
            sns.heatmap(pivot_table, cmap="coolwarm", linewidths=0.5)
            plt.title("Stock Price Heatmap")
        
        else:
            print("Invalid selection. Showing default line graph.")
            for stock in top_stocks:
                stock_data = df_selected[df_selected["Stock Symbol"] == stock]
                plt.plot(stock_data["Date"], stock_data["Close"], label=stock)
            plt.xlabel("Date")
            plt.ylabel("Price")
            plt.title("Stock Prices Over Time")
        
        plt.legend()
        plt.show()
        
        # Ask user if they want to analyze another range
        repeat = input("Would you like to analyze another range? (yes/no): ").strip().lower()
        if repeat != "yes":
            break

if __name__ == "__main__":
    analyze_stock_data()
