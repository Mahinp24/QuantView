import pandas as pd
import matplotlib.pyplot as plt
import numpy as np

# ==========================
# STOCK LIST
# ==========================
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

# ==========================
# CREATE MANUAL DATAFRAME
# ==========================
dates = pd.date_range(start="2026-03-01", end="2026-03-30")
df = pd.DataFrame(index=dates, columns=stocks)

# ==========================
# FUNCTION TO ENTER PRICE FOR A SPECIFIC STOCK AND DATE
# ==========================
def enter_price(stock_name, date):
    while True:
        try:
            price = float(input(f"💰 Enter price for {stock_name} on {date.date()}: $"))
            df.at[date, stock_name] = price
            break
        except ValueError:
            print("⚠️ Please enter a valid number.")

# ==========================
# INTERACTIVE VIEW FUNCTION
# ==========================
def quantview_interactive():
    print("\n🎉 Welcome to QuantView! Track your stocks from March 2026.\n")
    while True:
        print("📈 Available stocks:")
        for s in stocks:
            print("-", s)
stock_name = input("\nEnter stock name (or type 'exit' to quit): ")
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

# Prompt for price if missing
if pd.isna(df.at[date, stock_name]):
            enter_price(stock_name, date)

 # Calculate daily return if previous day exists
prev_date_idx = df.index.get_loc(date) - 1
        if prev_date_idx >= 0 and not pd.isna(df.iloc[prev_date_idx][stock_name]):
            prev_price = df.iloc[prev_date_idx][stock_name]
            daily_return = (df.at[date, stock_name] - prev_price) / prev_price
        else:
            daily_return = np.nan

        high = df[stock_name].max()
        low = df[stock_name].min()
        price = df.at[date, stock_name]
 # Display info with emojis
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

# Plot chart - colorful and fun
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

# ==========================
# RUN THE INTERACTIVE TOOL
# ==========================
quantview_interactive()
