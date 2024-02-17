class CoffeeMachine:
    def __init__(self):
        # Initialize the quantities of resources and money
        self.water = 500
        self.milk = 500
        self.coffee_beans = 200
        self.cups = 10
        self.money = 0

    def check_resources(self, water_needed, milk_needed, coffee_beans_needed, cups_needed):
        # Check if there are enough resources to make the selected coffee
        if self.water < water_needed:
            return "Sorry, not enough water."
        elif self.milk < milk_needed:
            return "Sorry, not enough milk."
        elif self.coffee_beans < coffee_beans_needed:
            return "Sorry, not enough coffee beans."
        elif self.cups < cups_needed:
            return "Sorry, not enough cups."
        else:
            return "Enough resources. Enjoy your coffee!"

    def buy_coffee(self, choice):
        if choice == "espresso":
            # Set the requirements and price for espresso
            water_needed = 50
            milk_needed = 0
            coffee_beans_needed = 18
            cups_needed = 1
            price = 15.00  # ₹15.00 for Espresso
            coffee_type = "Espresso"
        elif choice == "latte":
            # Set the requirements and price for latte
            water_needed = 200
            milk_needed = 150
            coffee_beans_needed = 24
            cups_needed = 1
            price = 25.00  # ₹25.00 for Latte
            coffee_type = "Latte"
        elif choice == "cappuccino":
            # Set the requirements and price for cappuccino
            water_needed = 250
            milk_needed = 100
            coffee_beans_needed = 24
            cups_needed = 1
            price = 30.00  # ₹30.00 for Cappuccino
            coffee_type = "Cappuccino"
        else:
            # Return an error message for invalid choices
            message = "Invalid choice. Please try again."
            return message

        # Check if there are enough resources to make the selected coffee
        message = self.check_resources(
            water_needed, milk_needed, coffee_beans_needed, cups_needed)
        if message == "Enough resources. Enjoy your coffee!":
            # Prompt for inserting coins and calculate the total amount
            print(f"Please insert coins for {coffee_type} (₹{price}):")
            five_rs = int(input("How many ₹5 coins?: "))
            two_rs = int(input("How many ₹2 coins?: "))
            one_rs = int(input("How many ₹1 coins?: "))
            fifty_paise = int(input("How many 50 paise coins?: "))

            total_amount = 5 * five_rs + 2 * two_rs + 1 * one_rs + 0.5 * fifty_paise
            if total_amount < price:
                return "Insufficient amount. Money refunded."
            else:
                # Calculate the change, update machine's properties, and return success message
                change = round(total_amount - price, 2)
                self.money += price
                self.water -= water_needed
                self.milk -= milk_needed
                self.coffee_beans -= coffee_beans_needed
                self.cups -= cups_needed
                return f"Here is ₹{change} in change. Here is your {coffee_type}. Enjoy!"

        # Return the error message if there are insufficient resources
        return message


def main():
    # Create an instance of the CoffeeMachine class
    coffee_machine = CoffeeMachine()

    while True:
        print("============================================")
        choice = input("What would you like? (espresso/latte/cappuccino): ")

        if choice in ["espresso", "latte", "cappuccino"]:
            print(coffee_machine.buy_coffee(choice))
        else:
            print("Invalid choice. Please try again.")


if __name__ == "__main__":
    main()
