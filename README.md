import pandas as pd
import matplotlib.pyplot as plt
import numpy as np

# STOCK LIST
stocks = [
    "🍎 Apple",
    "🛒 Amazon",
    "💻 Nvidia",
    "🔍 Google",
    "🏪 Walmart",
    "👑 Louis Vuitton",
    "🚗 Tesla",
    "🏦 JP Morgan",
    "🛍️ Costco",
    "📺 Netflix"
]

# CREATE DATAFRAME FOR MARCH 2026
dates = pd.date_range(start="2026-03-01", end="2026-03-30")
df = pd.DataFrame(index=dates, columns=stocks)

# FUNCTION TO ENTER PRICE MANUALLY
def enter_price(stock_name, date):
    while True:
        try:
            price = float(input(f"💰 Enter price for {stock_name} on {date.date()}: $"))
            df.at[date, stock_name] = price
            break
        except ValueError:
            print("⚠️ Invalid input! Please enter a number.")

# INTERACTIVE TOOL
def quantview():
    print("\n🎉 Welcome to QuantView! Track your stocks from March 2026.\n")

while True:
print("📈 Available stocks:")
for s in stocks:
     print("-", s)
stock_name = input("\nEnter stock name (or 'exit' to quit): ")
if stock_name.lower() == "exit":
    print("👋 Thanks for using QuantView! Goodbye!")
    break
if stock_name not in stocks:
        print("⚠️ Stock not found! Try again.\n")
    continue

date_input = input("📅 Enter date (YYYY-MM-DD, e.g., 2026-03-15): ")
        try:
    date = pd.Timestamp(date_input)
    if date not in df.index:
        print("⚠️ Date out of range. Please pick between 2026-03-01 and 2026-03-30.\n")
                continue
except:
    print("⚠️ Invalid date format. Try again.\n")
            continue

# Enter price if missing
if pd.isna(df.at[date, stock_name]):
            enter_price(stock_name, date)

# Daily return
prev_idx = df.index.get_loc(date) - 1
     if prev_idx >= 0 and not pd.isna(df.iloc[prev_idx][stock_name]):
        prev_price = df.iloc[prev_idx][stock_name]
        daily_return = (df.at[date, stock_name] - prev_price) / prev_price
        else:
            daily_return = np.nan

 # High / low
high = df[stock_name].max()
low = df[stock_name].min()
price = df.at[date, stock_name]

# Print info
print(f"\n🌟========== QuantView ==========")
        print(f"📌 Stock: {stock_name}")
        print(f"🗓 Date: {date.date()}")
        print(f"💵 Price for 1 share: ${price}")
        if not np.isnan(daily_return):
            print(f"📊 Daily Return: {daily_return*100:.2f}%")
        else:
            print("📊 Daily Return: N/A (first day or missing previous price)")
        print(f"⬆️ Highest Price in Month: ${high}")
        print(f"⬇️ Lowest Price in Month: ${low}")
        print(f"🌟==============================\n")

# Plot chart
plt.figure(figsize=(12,6))
        plt.plot(df[stock_name], color="#ff7f0e", linewidth=3, marker='o', markersize=6, label=stock_name)
        plt.title(f"📈 QuantView: {stock_name} Price March 2026", fontsize=16, fontweight='bold', color="#2c3e50")
        plt.xlabel("Date", fontsize=12, color="#34495e")
        plt.ylabel("Price ($)", fontsize=12, color="#34495e")
        plt.grid(True, linestyle='--', alpha=0.5)
        plt.xticks(rotation=45)
        plt.legend()
        plt.tight_layout()
        plt.show()

# RUN TOOL
if __name__ == "__main__":
    quantview()


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
            price = df.loc[date, stock
            
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
