# Stock-Portfolio-Tracker
import csv

# Hardcoded stock prices
STOCK_PRICES = {
    "AAPL": 180.5,
    "TSLA": 250.0,
    "GOOGL": 140.2,
    "AMZN": 175.0,
    "MSFT": 400.0
}

def stock_tracker():
    print("=== Stock Portfolio Tracker ===")
    portfolio = {}

    while True:
        symbol = input("\nEnter Stock Symbol (e.g. AAPL, TSLA) or type 'done' to finish: ").upper().strip()
        
        if symbol == 'DONE':
            break

        if symbol not in STOCK_PRICES:
            print(f"Stock '{symbol}' not found in database. Available stocks: {list(STOCK_PRICES.keys())}")
            continue

        try:
            quantity = int(input(f"Enter quantity for {symbol}: "))
            if quantity <= 0:
                print("Quantity must be greater than zero.")
                continue
            
            portfolio[symbol] = portfolio.get(symbol, 0) + quantity
        except ValueError:
            print("Invalid input. Please enter a valid number for quantity.")

    if not portfolio:
        print("No stocks added to portfolio.")
        return

    # Calculate Total
    total_investment = 0.0
    print("\n--- Your Investment Summary ---")
    for symbol, quantity in portfolio.items():
        price = STOCK_PRICES[symbol]
        subtotal = price * quantity
        total_investment += subtotal
        print(f"{symbol}: {quantity} shares x ${price} = ${subtotal:.2f}")

    print(f"\nTotal Portfolio Value: ${total_investment:.2f}")

    # Optional: Save to CSV File
    save_option = input("\nDo you want to save this report to a CSV file? (yes/no): ").lower().strip()
    if save_option in ['yes', 'y']:
        filename = "portfolio_summary.csv"
        with open(filename, mode='w', newline='') as file:
            writer = csv.writer(file)
            writer.writerow(["Stock Symbol", "Quantity", "Price per Share ($)", "Total Value ($)"])
            for symbol, quantity in portfolio.items():
                price = STOCK_PRICES[symbol]
                writer.writerow([symbol, quantity, price, price * quantity])
            writer.writerow([])
            writer.writerow(["Total Portfolio Value", "", "", total_investment])
        print(f"Report successfully saved to {filename}")

if __name__ == "__main__":
    stock_tracker()# Stock-Portfolio-Tracker
