import tkinter as tk

class BankAccount:
    def _init_(self, account_number, account_holder, initial_balance=0):
        self.account_number = account_number
        self.account_holder = account_holder
        self.balance = initial_balance

    def deposit(self, amount):
        if amount > 0:
            self.balance += amount
            l4.config(text=f"Deposited Rs{amount}. New balance: Rs{self.balance}")
        else:
            l4.config(text="Invalid amount. Please enter a positive value")

    def withdraw(self, amount):
        if amount > 0 and amount <= self.balance:
            self.balance -= amount
            l5.config(text=f"Withdrew Rs{amount}. New balance is Rs{self.balance}")
        elif amount <= 0:
            l5.config(text="Invalid amount. Please enter a positive value")
        else:
            l5.config(text="Insufficient balance")

    def check_balance(self):
        l5.config(text=f"Account balance for {self.account_holder}: Rs{self.balance}")

def check_balance1():
    account_number = t1.get()
    account = accounts.get(account_number, None)
    if account:
        account.check_balance()
    else:
        l5.config(text="Account not found")

def deposit_money():
    account_number = t1.get()
    account = accounts.get(account_number, None)
    if account:
        amount = float(t3.get())
        account.deposit(amount)
    else:
        l4.config(text="Account not found")

def withdraw_money():
    account_number = t1.get()
    account = accounts.get(account_number, None)
    if account:
        amount = float(t3.get())
        account.withdraw(amount)
    else:
        l4.config(text="Account not found")

def register_account():
    account_number = t1.get()
    username = t2.get()
    initial_balance = float(t3.get())
    accounts[account_number] = BankAccount(account_number, username, initial_balance)

# Create a dictionary to store accounts
accounts = {}

root = tk.Tk()
root.title("Banking App")

# Define labels and entry fields
l1 = tk.Label(root, text="Account number")
l2 = tk.Label(root, text="User name")
l3 = tk.Label(root, text="Amount")
t1 = tk.Entry(root)
t2 = tk.Entry(root)
t3 = tk.Entry(root)

# Define buttons
b1 = tk.Button(root, text="Register Account", command=register_account)
b2 = tk.Button(root, text="View Balance", command=check_balance1)
b3 = tk.Button(root, text="Deposit", command=deposit_money)
b4 = tk.Button(root, text="Withdraw", command=withdraw_money)

# Place widgets on the grid
l1.grid(row=0, column=0)
l2.grid(row=1, column=0)
l3.grid(row=2, column=0)
t1.grid(row=0, column=1)
t2.grid(row=1, column=1)
t3.grid(row=2, column=1)
b1.grid(row=3, column=1)
b2.grid(row=4, column=1)
b3.grid(row=5, column=1)
b4.grid(row=6, column=1)

# Initialize labels for displaying messages
l4 = tk.Label(root, text="", fg="green")
l4.grid(row=7, column=1)
l5 = tk.Label(root, text="", fg="green")
l5.grid(row=8, column=1)

# Start the tkinter main loop
tk.mainloop()
