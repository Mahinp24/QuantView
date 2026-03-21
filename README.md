import yfinance as yf
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt

# ------------------------
# STOCK LIST
# ------------------------
stocks = {
    "Apple": "AAPL",
    "Amazon": "AMZN",
    "Nvidia": "NVDA",
    "Google": "GOOGL",
    "Walmart": "WMT",
    "Louis Vuitton": "MC.PA",
    "Tesla": "TSLA",
    "JP Morgan": "JPM",
    "Costco": "COST",
    "Netflix": "NFLX"
}

# ------------------------
# DOWNLOAD HISTORICAL DATA
# ------------------------
start_date = "2026-03-01"
end_date = "2026-03-30"

data = {}
for name, ticker in stocks.items():
    stock_data = yf.download(ticker, start=start_date, end=end_date)
    data[name] = stock_data['Adj Close']

# Combine all stocks into one DataFrame
df = pd.DataFrame(data)

# ------------------------
# DAILY RETURNS
# ------------------------
daily_returns = df.pct_change().dropna()

# ------------------------
# SHARPE RATIOS (annualized, risk-free rate = 0)
# ------------------------
sharpe_ratios = (daily_returns.mean() / daily_returns.std()) * np.sqrt(252)

# ------------------------
# HIGHS AND LOWS
# ------------------------
highs = df.max()
lows = df.min()

# ------------------------
# INTERACTIVE FUNCTION
# ------------------------
def view_stock(stock_name, date):
    if stock_name not in df.columns:
        print("Stock not found!")
        return
    
try:
        price = df.loc[date, stock_name]
        daily_return = daily_returns.loc[date, stock_name]
        sharpe = sharpe_ratios[stock_name]
        high = highs[stock_name]
        low = lows[stock_name]

print(f"----- {stock_name} on {date} -----")
        print(f"Price for 1 share: ${price:.2f}")
        print(f"Daily Return: {daily_return*100:.2f}%")
        print(f"Sharpe Ratio (annualized): {sharpe:.2f}")
        print(f"Highest Price in March: ${high:.2f}")
        print(f"Lowest Price in March: ${low:.2f}")
        print("-------------------------------")

# Plot the stock price chart
df[stock_name].plot(title=f"{stock_name} Price March 2026")
        plt.xlabel("Date")
        plt.ylabel("Price ($)")
        plt.show()

 except KeyError:
        print("Date not available in the dataset!")

# ------------------------
# EXAMPLE USAGE
# ------------------------
# Pick a stock and a date
stock_to_check = "Amazon"
date_to_check = "2026-03-15"

view_stock(stock_to_check, date_to_check)
