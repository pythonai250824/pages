## 🏦 Exercise: `BankAccount` Class 

<img src="oop4_uml.jpg" />

Create a class named `BankAccount` that represents a simple bank account with:

- `owner`: the name of the account holder (string)
- `balance`: how much money is in the account (float)

### 1. Constructor
```python
def __init__(self, owner: str, balance: float)
```

### 2. Class Variable and Class Method

- Add a **private class variable** for the bank's address:  
  `"1 Allenby St, Tel Aviv"` (actual Discount Bank branch)

- Add a **class method**:
  ```python
  @classmethod
  def get_bank_address(cls) -> str
  ```
  Returns the bank address.

### 3. Static Method

Add a static method:
```python
@staticmethod
def highest_balance(acc1: "BankAccount", acc2: "BankAccount", acc3: "BankAccount") -> float
```

- Return the highest balance among the three accounts.
- No use of `self` or `cls` — it’s a utility.

Example:
```python
a1 = BankAccount("A", 300)
a2 = BankAccount("B", 700)
a3 = BankAccount("C", 500)
print(BankAccount.highest_balance(a1, a2, a3))  # → 700.0
```

### 4. Properties (Getters and Setters)

Use `@property` to create:

- `owner` – read-only
- `balance` – readable and writeable

### 5. Methods

- `deposit(self, amount: float) -> None`
- `withdraw(self, amount: float) -> None`
- `is_rich(self) -> bool` : return True if the balance is larger than 1M otherwise False

### 6. Operator Overloading

- `__add__(self, other)`  
  - Add two accounts → if owners differ, return `"Joint: A & B"`  
  - Add number → return new account with increased balance

- `__sub__(self, other)`  
  - Subtract another account or number → return new account

- `__eq__(self, other)`  
  - Compare owner and balance  
  - Also support comparing with a number or tuple

- `__ne__`, `__gt__`, `__ge__`, `__lt__`, `__le__` → compare balance only

- `__repr__`, `__str__`  
- `__len__()` → rounded balance  
- `__getitem__(key)` → 'owner', 'balance', 0, 1  
- `__iter__()` → yields owner, balance

### 7. Bonus Feature 💡

```python
def freeze(self) -> None
```
Sets:
- `owner = "FROZEN"`
- `balance = 0.0`

### 8. Demo Code

Test all features, including:
```python
# --- Demo Code for BankAccount class ---

# Create accounts
acc1 = BankAccount("Alice", 800.0)
acc2 = BankAccount("Bob", 1200.0)
acc3 = BankAccount("Alice", 800.0)
acc4 = BankAccount("Charlie", 300.0)

# Test __repr__ / __str__
print("Accounts:")
print(acc1)
print(acc2)
print(acc3)

# Test __eq__ (same owner and balance)
print("\nEquality:")
print("acc1 == acc3:", acc1 == acc3)  # True
print("acc1 == acc2:", acc1 == acc2)  # False
print("acc1 == 800:", acc1 == 800)    # True
print("acc1 == ('Alice', 800):", acc1 == ("Alice", 800))  # True

# Test __ne__
print("\nInequality:")
print("acc1 != acc2:", acc1 != acc2)  # True

# Test __gt__ (based on balance)
print("\nGreater Than:")
print("acc2 > acc1:", acc2 > acc1)  # True
print("acc4 > acc1:", acc4 > acc1)  # False

# Test __lt__, __ge__, __le__
print("\nOther comparisons:")
print("acc1 < acc2:", acc1 < acc2)  # True
print("acc2 >= acc1:", acc2 >= acc1)  # True
print("acc4 <= acc1:", acc4 <= acc1)  # True

# Test __add__ (same owner)
print("\nAdd:")
acc5 = acc1 + acc3
print("acc5 (Alice + Alice):", acc5)

# Test __add__ (different owners)
acc6 = acc1 + acc2
print("acc6 (Alice + Bob):", acc6)

# Test __add__ with number
acc7 = acc1 + 200
print("acc1 + 200:", acc7)

# Test __sub__ with another account
acc8 = acc2 - acc1
print("acc2 - acc1:", acc8)

# Test __sub__ with number
acc9 = acc2 - 500
print("acc2 - 500:", acc9)

# Test __getitem__
print("\nGet item:")
print("acc1['owner']:", acc1['owner'])
print("acc1[1]:", acc1[1])  # balance

# Test __iter__
print("\nIterating acc1:")
for info in acc1:
    print(info)

# Test __len__
print("\nLength of acc1:", len(acc1))

# Test class method
print("\nBank address:", BankAccount.get_bank_address())

# Test static method
print("\nHighest balance:", BankAccount.highest_balance(acc1, acc2, acc4))

```

