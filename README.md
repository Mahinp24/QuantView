# ==========================
# QUANTVIEW - SIMPLE STOCK ANALYZER
# No external libraries required
# ==========================

# STOCK LIST
STOCKS = {
    "1": "Apple 🍎",
    "2": "Amazon 🛒",
    "3": "Nvidia 💻",
    "4": "Google 🔍",
    "5": "Walmart 🏪",
    "6": "Louis Vuitton 👑",
    "7": "Tesla 🚗",
    "8": "JP Morgan 🏦",
    "9": "Costco 🛍️",
    "10": "Netflix 📺"
}

# STORAGE FOR USER INPUT DATA
data_store = {}

# ==========================
# SIGNAL FUNCTION
# ==========================
def get_signal(price, low, high):
    if price <= low * 1.05:
        return "🟢 BUY (undervalued zone)"
    elif price >= high * 0.95:
        return "🔴 SELL (overvalued zone)"
    else:
        return "🟡 HOLD (neutral zone)"

# ==========================
# INPUT STOCK DATA
# ==========================
def input_data(stock_name):
    print("\n📊 Enter market data for", stock_name)

 price = float(input("💰 Current price (1 share): $"))
    high = float(input("📈 Highest price: $"))
    low = float(input("📉 Lowest price: $"))

ratio = (price - low) / (high - low + 0.000001)

data_store[stock_name] = {
        "price": price,
        "high": high,
        "low": low,
        "ratio": ratio
    }

# ==========================
# DISPLAY REPORT
# ==========================
def show_report(stock_name):
    d = data_store[stock_name]

 print("\n" + "=" * 40)
    print(f"📊 QUANTVIEW ANALYSIS: {stock_name}")
    print("=" * 40)
    print(f"💰 Price (1 share): ${d['price']:.2f}")
    print(f"📈 Highest Price: ${d['high']:.2f}")
    print(f"📉 Lowest Price: ${d['low']:.2f}")
    print(f"📊 Strength Ratio: {d['ratio']:.3f}")
    print(f"📍 Recommendation: {get_signal(d['price'], d['low'], d['high'])}")
    print("=" * 40 + "\n")

# ==========================
# MENU DISPLAY
# ==========================
def show_menu():
    print("\n📊 QUANTVIEW STOCK ANALYZER")
    print("-" * 40)
 for key in STOCKS:
        print(f"{key}. {STOCKS[key]}")
print("0. Exit")

# ==========================
# MAIN PROGRAM
# ==========================
def main():
    print("\n🚀 Welcome to QuantView")
    print("Simple Stock Decision System\n")

while True:
        show_menu()

choice = input("\nSelect a stock number: ")

if choice == "0":
            print("\n👋 Exiting QuantView... Goodbye!")
            break

if choice not in STOCKS:
            print("❌ Invalid choice. Try again.")
            continue

stock_name = STOCKS[choice]

# If not entered yet, request data
if stock_name not in data_store:
            input_data(stock_name)

# Show results
 show_report(stock_name)

# RUN PROGRAM
if __name__ == "__main__":
    main()
