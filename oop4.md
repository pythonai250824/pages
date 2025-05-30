## 🏦 Exercise: `BankAccount` Class

Create a class named `BankAccount` that represents a simple bank account with:

- `owner`: the name of the account holder (string)
- `balance`: how much money is in the account (float)

---

### 1. Constructor
```python
def __init__(self, owner: str, balance: float)
```

---

### 2. Properties (Getters and Setters)

Use `@property` to create:

- `owner` – read-only
- `balance` – readable and writeable

---

### 3. Methods

- `deposit(self, amount: float) -> None`  
  Add money to the balance

- `withdraw(self, amount: float) -> None`  
  Subtract money (only if there’s enough)

- `is_rich(self) -> bool`  
  Return `True` if balance is at least 1,000,000

- `@staticmethod def zero_account(owner: str) -> "BankAccount"`  
  Create an account with balance 0

---

### 4. Operator Overloading

- `__add__(self, other)`  
  You can:
  - Add **two BankAccount objects**:
    - If owners are the **same**, return a new account with the **same owner** and combined balance
    - If owners are **different**, return a new account with:
      - `owner = "Joint: A & B"` (in original order)
      - `balance = combined balance`
      - Example:
        ```python
        a1 = BankAccount("John", 200.0)
        a2 = BankAccount("Kate", 300.0)
        print(a1 + a2)
        # BankAccount(owner='Joint: John & Kate', balance=500.0)
        ```

  - Add a **number** to a BankAccount → return a new account with the same owner and increased balance

- `__sub__(self, other)`  
  - Subtract two accounts → return new account with difference in balance (no negatives)
  - Subtract a number → return new account with decreased balance

- `__eq__(self, other)`  
  Return `True` if:
  - Same owner **and**
  - Same balance

  Also allow comparing with:
  - A number (only balance is checked)
  - A tuple like `("John", 200.0)`

- `__ne__`, `__gt__`, `__ge__`, `__lt__`, `__le__`  
  Compare based on balance only

- `__repr__`, `__str__`  
  Show nicely as:
  ```python
  BankAccount(owner='Alice', balance=500.00)
  ```

- `__len__()`  
  Return the **rounded int** of the balance

- `__getitem__(key)`  
  Support:
  - `"owner"` or `0` → return owner
  - `"balance"` or `1` → return balance

- `__iter__()`  
  Yield: owner, then balance

---

### 5. Bonus Feature 💡
Add a method:
```python
def freeze(self) -> None
```
This sets:
- `owner = "FROZEN"`
- `balance = 0.0`

---

### 6. Demo Code

At the bottom of the file, write code that:

- Creates at least **3 accounts**
- Tests all methods and operators
- Prints results clearly

---

### 📦 UML: BankAccount

```
|-----------------------------|
|        BankAccount          |
|-----------------------------|
| - __owner: str              |
| - __balance: float          |
|-----------------------------|
| + __init__(owner, balance) |
| + owner: str                |
| + balance: float            |
| + deposit(amount): None     |
| + withdraw(amount): None    |
| + is_rich(): bool           |
| + zero_account(owner): BankAccount |
| + __add__(other)            |
| + __sub__(other)            |
| + __eq__(other)             |
| + __ne__(other)             |
| + __gt__(other)             |
| + __ge__(other)             |
| + __lt__(other)             |
| + __le__(other)             |
| + __repr__(), __str__()     |
| + __len__()                 |
| + __getitem__(key)          |
| + __iter__()                |
| + freeze()                  |
|-----------------------------|
```
