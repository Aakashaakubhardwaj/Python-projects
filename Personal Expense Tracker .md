import datetime

def get_expense_details():

  category = input("Enter expense category: ")
  amount = float(input("Enter expense amount: "))
  description = input("Enter expense description: ")

  return {
      "category": category,
      "amount": amount,
      "description": description
  }

expenses = []

num_expenses = int(input("Enter the number of expenses to add: "))
for _ in range(num_expenses):
  expense_details = get_expense_details()
  expense_details['date'] = datetime.date.today().isoformat()
  expenses.append(expense_details)


print(expenses) 

def display_expenses(expenses):

  for expense in expenses:
    print(expense)
    
display_expenses(expenses)


def get_monthly_budget():

  while True:
    try:
      budget = float(input("Enter your monthly budget: "))
      if budget > 0: 
        return budget
      else:
        print("Invalid input. Budget must be a positive number.")
    except ValueError:
      print("Invalid input. Please enter a number.")

# Example usage:
monthly_budget = get_monthly_budget()
print(f"Your monthly budget is: {monthly_budget}")

def calculate_expenses_and_balance(expenses, budget):
  total_expenses = sum(expense['amount'] for expense in expenses)

  if total_expenses <= budget:
    remaining_balance = budget - total_expenses
    print(f"Total budget: {monthly_budget}")
    print(f"Total expenses: {total_expenses}")  
    print(f"Remaining balance: {remaining_balance}")  
  else:
    print(f"Total expenses: {total_expenses}") 
    print("You have exceeded your budget.") 


calculate_expenses_and_balance(expenses, monthly_budget)


import csv

def save_expenses_to_csv(expenses, filename="expenses.csv"): 
  with open(filename, 'w', newline='') as csvfile:
    fieldnames = ['date', 'category', 'amount', 'description']
    writer = csv.DictWriter(csvfile, fieldnames=fieldnames)

    writer.writeheader()
    writer.writerows(expenses)

  print(f"Expenses saved to {filename}")

save_expenses_to_csv(expenses)
save_expenses_to_csv(expenses, "my_expenses.csv")

def load_expenses_from_csv(filename="expenses.csv"):

  expenses = []
  with open(filename, 'r', newline='') as csvfile:
    reader = csv.DictReader(csvfile)
    for row in reader:
      # Convert amount to float
      row['amount'] = float(row['amount']) 
      expenses.append(row)
  return expenses
expenses = load_expenses_from_csv()
expenses

def display_menu():
  """Displays a menu of options for the expense tracker."""

  print("\nExpense Tracker Menu:")
  print("1. Add expense")
  print("2. Display expenses")
  print("3. Calculate expenses and balance")
  print("4. Save expenses to CSV")
  print("5. Load expenses from CSV")
  print("6. Exit")

def main():
 expenses = load_expenses_from_csv() 
 monthly_budget = 90000.0

 while True:

    display_menu()
    try:
      choice = int(input("Enter your choice (1-6): "))  # integer input

      if choice == 1:
        expense_details = get_expense_details()
        expense_details['date'] = datetime.date.today().isoformat()
        expenses.append(expense_details)
        print("Expense added successfully!")
  
      elif choice == 2:
        display_expenses(expenses)
      elif choice == 3:
        calculate_expenses_and_balance(expenses, monthly_budget)
      elif choice == 4:
        save_expenses_to_csv(expenses)
      elif choice == 5:
        expenses = load_expenses_from_csv()
      elif choice == 6:
        break
      else:
        print("Invalid choice. Please enter a number between 1 and 6.")
    except ValueError:
      print("Invalid input. Please enter a number.")

if __name__ == "__main__":
  main()


load_expenses_from_csv()
