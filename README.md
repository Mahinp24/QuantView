import yfinance as yf
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt

# Stock tickers
stocks = {
    "Apple": "AAPL",
    "Amazon": "AMZN",
    "Nvidia": "NVDA",
    "Google": "GOOGL",
    "Walmart": "WMT",
    "Louis Vuitton": "LVMUY",
    "Tesla": "TSLA",
    "JP Morgan": "JPM",
    "Costco": "COST",
    "Netflix": "NFLX"
}

start_date = "2026-03-01"
end_date = "2026-03-30"

def get_stock_data(ticker):
    data = yf.download(ticker, start=start_date, end=end_date)
    return data

def calculate_daily_returns(data):
    data["Daily Return"] = data["Adj Close"].pct_change()
    return data

def calculate_sharpe_ratio(data):
    sharpe = (data["Daily Return"].mean() / data["Daily Return"].std()) * np.sqrt(252)
    return sharpe

def get_high_low(data):
    highest = data["Adj Close"].max()
    lowest = data["Adj Close"].min()
    return highest, lowest

def plot_chart(data, stock_name):
    plt.figure()
    plt.plot(data["Adj Close"])
    plt.title(stock_name + " Price Trend (March 2026)")
    plt.xlabel("Date")
    plt.ylabel("Price ($)")
    plt.show()

def analyze_stock(name, ticker):
    data = get_stock_data(ticker)
    data = calculate_daily_returns(data)

  sharpe = calculate_sharpe_ratio(data)
    high, low = get_high_low(data)

  print("\nStock:", name)
    print("Sharpe Ratio:", sharpe)
    print("Highest Price:", high)
    print("Lowest Price:", low)

  plot_chart(data, name)

def main():
    print("Stock Analyzer")

  for name, ticker in stocks.items():
        analyze_stock(name, ticker)

main()
