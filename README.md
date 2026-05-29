# ==========================
# QUANTVIEW MEMORY SYSTEM
# ==========================

stocks = {
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

# STORAGE (memory system)
stock_memory = {}

# ==========================
# SIGNAL LOGIC
# ==========================
def signal(price, low, high):
    if price <= low * 1.05:
        return "🟢 BUY (undervalued)"
    elif price >= high * 0.95:
        return "🔴 SELL (overvalued)"
    else:
        return "🟡 HOLD (stable)"

# ==========================
# INPUT DATA (STORE ONCE)
# ==========================
def input_data(stock_name):
    print(f"\n📥 Enter data for {stock_name}")

price = float(input("💰 Price (1 share): $"))
high = float(input("📈 Highest price: $"))
low = float(input("📉 Lowest price: $"))

ratio = (price - low) / (high - low + 1e-9)

# STORE IN MEMORY
stock_memory[stock_name] = {
        "price": price,
        "high": high,
        "low": low,
        "ratio": ratio
    }

print("✅ Data saved successfully!\n")

# ==========================
# RECALL DATA (MAIN FEATURE)
# ==========================
def show_data(stock_name):

data = stock_memory[stock_name]

 print("\n━━━━━━━━━━━━━━━━━━━━━━━━━━━━")
    print(f"📊 QUANTVIEW ANALYSIS: {stock_name}")
    print("━━━━━━━━━━━━━━━━━━━━━━━━━━━━")
    print(f"💰 1 Share Price: ${data['price']:.2f}")
    print(f"📈 Highest: ${data['high']:.2f}")
    print(f"📉 Lowest: ${data['low']:.2f}")
    print(f"📊 Strength Ratio: {data['ratio']:.3f}")
    print(f"📍 Signal: {signal(data['price'], data['low'], data['high'])}")
    print("━━━━━━━━━━━━━━━━━━━━━━━━━━━━\n")

# ==========================
# MENU
# ==========================
def menu():
    print("\n📊 QUANTVIEW STOCK SYSTEM")
    print("-" * 40)

for key in stocks:
        print(f"{key}. {stocks[key]}")

print("0. Exit")

# ==========================
# MAIN LOOP
# ==========================
def quantview():

print("\n🚀 Welcome to QuantView Memory System")
    print("Store data once → recall anytime\n")

while True:

 menu()
        choice = input("\nSelect a stock number: ")

if choice == "0":
            print("👋 Exiting QuantView...")
            break

 if choice not in stocks:
            print("❌ Invalid selection\n")
            continue

stock_name = stocks[choice]

# IF NOT STORED → INPUT DATA
if stock_name not in stock_memory:
            input_data(stock_name)

 # ALWAYS RECALL DATA
 show_data(stock_name)

# RUN PROGRAM
if __name__ == "__main__":
    quantview()
