import pandas as pd
import numpy as np

# ==========================
# STOCK LIST
# ==========================
stocks = {
    "Apple 🍎": "AAPL",
    "Amazon 🛒": "AMZN",
    "Nvidia 💻": "NVDA",
    "Google 🔍": "GOOGL",
    "Walmart 🏪": "WMT",
    "Louis Vuitton 👑": "MC.PA",
    "Tesla 🚗": "TSLA",
    "JP Morgan 🏦": "JPM",
    "Costco 🛍️": "COST",
    "Netflix 📺": "NFLX"
}

# ==========================
# CREATE EMPTY DATA (YOU FILL LATER)
# ==========================
dates = pd.date_range("2026-03-01", "2026-03-30")
df = pd.DataFrame(index=dates, columns=stocks.keys())

# ==========================
# INPUT PRICE FUNCTION
# ==========================
def input_price(stock, date):
    while True:
        try:
            price = float(input(f"💰 Enter price for {stock} on {date.date()}: $"))
            df.loc[date, stock] = price
            return price
        except:
            print("❌ Invalid number, try again.")

# ==========================
# BUY / SELL SIGNAL (SIMPLE LOGIC)
# ==========================
def signal(current, low, high):
    if current <= low * 1.05:
        return "🟢 BUY (near monthly low)"
    elif current >= high * 0.95:
        return "🔴 SELL (near monthly high)"
    else:
        return "🟡 HOLD"

# ==========================
# MAIN PROGRAM
# ==========================
def quantview():

print("\n📊 WELCOME TO QUANTVIEW 📊")
    print("Track stock prices, trends, and signals (March 2026)\n")
    while True:

  # ================= STOCK SELECTION =================
 print("\n📈 Select a stock:")
        stock_list = list(stocks.keys())

for i, s in enumerate(stock_list):
            print(f"{i+1}. {s}")

print("0. Exit")

try:
            choice = int(input("\nEnter stock number: "))
            if choice == 0:
                print("👋 Exiting QuantView...")
                break
            stock = stock_list[choice - 1]
        except:
            print("❌ Invalid selection")
            continue

 # ================= DATE SELECTION =================
print("\n📅 Enter date (2026-03-01 to 2026-03-30)")
        date_input = input("Format YYYY-MM-DD: ")

try:
            date = pd.Timestamp(date_input)
            if date not in df.index:
                print("❌ Date not in range")
                continue
        except:
            print("❌ Invalid date format")
            continue

 # ================= PRICE INPUT =================
if pd.isna(df.loc[date, stock]):
            price = input_price(stock, date)
        else:
            price = df.loc[date, stock]

 # ================= CALCULATIONS =================
 col = df[stock]

low = col.min()
high = col.max()

 prev_idx = df.index.get_loc(date) - 1
        if prev_idx >= 0 and not pd.isna(col.iloc[prev_idx]):
            prev_price = col.iloc[prev_idx]
            daily_return = ((price - prev_price) / prev_price) * 100
        else:
            daily_return = 0

  # ================= OUTPUT =================
 print("\n━━━━━━━━━━━━━━━━━━━━━━━━━━━━")
        print(f"📊 QUANTVIEW REPORT: {stock}")
        print("━━━━━━━━━━━━━━━━━━━━━━━━━━━━")
        print(f"📅 Date: {date.date()}")
        print(f"💰 Price (1 share): ${price:.2f}")
        print(f"📊 Daily Return: {daily_return:.2f}%")
        print(f"📈 Monthly High: ${high}")
        print(f"📉 Monthly Low: ${low}")
        print(f"📍 Signal: {signal(price, low, high)}")
        print("━━━━━━━━━━━━━━━━━━━━━━━━━━━━\n")

# ==========================
# RUN PROGRAM
# ==========================
quantview()
