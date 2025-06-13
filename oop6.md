# 💳 Exercise: Payment System with Source Verification

## 📆 Instructions

> Implement a payment system that validates transactions based on their source (credit card or PayPal).
> The system should use **abstract classes**, **inheritance**, and **interfaces** for clean design and separation of concerns.

### 🌟 Learning Goals

* Implement and inherit from an abstract base class
* Implement multiple interfaces (e.g., for verification)
* Validate transactions using external input (credit card number or email)

### 🧱 Requirements

#### 1. Interfaces

* `ITransfer`
  Method:

  ```python
  transfer(amount: float, to_account: BankAccount) -> bool
  ```

* `IVerifyCreditCard`
  Method:

  ```python
  verify_credit_card(card_number: str) -> bool
  ```

* `IVerifyPayPal`
  Method:

  ```python
  verify_paypal_email(email: str) -> bool
  ```

#### 2. Class: `BankAccount`

* Fields:

  * `id: str`
  * `balance: float`
  * `credit_card_number: Optional[str]`
  * `paypal_email: Optional[str]`

* Implements:

  * `ITransfer`
  * `IVerifyCreditCard`
  * `IVerifyPayPal`

* Methods:

  * `transfer(...)` – performs the money transfer if balance is sufficient
  * `verify_credit_card(...)` – returns True if matches internal number
  * `verify_paypal_email(...)` – returns True if matches internal email

#### 3. Abstract Class: `Payment`

* Fields:

  * `amount: float`
  * `from_account_id: str`
  * `to_account_id: str`

* Method:

  * `process() -> bool` *(abstract)*

#### 4. Derived Classes

* `CreditCardPayment`:

  * Additional field: `card_number: str`
  * In `process()`:

    * Verifies `from_account` implements `IVerifyCreditCard`
    * Calls `verify_credit_card()`
    * If successful, proceeds with `transfer(...)`

* `PayPalPayment`:

  * Additional field: `email: str`
  * In `process()`:

    * Verifies `from_account` implements `IVerifyPayPal`
    * Calls `verify_paypal_email()`
    * If successful, proceeds with `transfer(...)`

## 📊 UML (Text-Based)

```
<<interface>>         <<interface>>                 <<interface>>
+--------------+      +------------------------+    +------------------------------+
| ITransfer    |      | IVerifyCreditCard      |    | IVerifyPayPal                |
+--------------+      +------------------------+    +------------------------------+
| + transfer() |      | + verify_credit_card() |    | + verify_paypal_email...()   |
+--------------+      +------------------------+    +------------------------------+

                             ▲
                      +-----------------------------+
                      |         BankAccount         |
                      +-----------------------------+
                      | - id: str                   |
                      | - balance: float            |
                      | - credit_card_number: str?  |
                      | - paypal_email: str?        |
                      +-----------------------------+
                      | + transfer(...)             |
                      | + verify_credit_card(...)   |
                      | + verify_paypal_email(...)  |
                      +-----------------------------+

                <<abstract>>
              +------------------------+
              |        Payment         |
              +------------------------+
              | - amount: float        |
              | - from_account_id: str |
              | - to_account_id: str   |
              +------------------------+
              | # process()            |   <<abstract>>
              +------------------------+
                         ▲
               +---------+------------+
               |                      |
+--------------------------+   +------------------------+
|   CreditCardPayment      |   |     PayPalPayment      |
+--------------------------+   +------------------------+
| - card_number: str       |   | - email: str           |
| + process()              |   | + process()            |
+--------------------------+   +------------------------+
```

---

## 📝 Example `main()` Code

```python
def main():
    accounts = {
        "A001": BankAccount("A001", 1000.0, credit_card_number="1234567890123456", paypal_email="user1@example.com"),
        "A002": BankAccount("A002", 500.0, credit_card_number="1111222233334444", paypal_email="user2@example.com")
    }

    payments = [
        CreditCardPayment(200.0, "A001", "A002", card_number="1234567890123456"),  # valid
        PayPalPayment(300.0, "A001", "A002", email="wrong@example.com"),           # invalid email
        CreditCardPayment(900.0, "A002", "A001", card_number="1111222233334444")   # insufficient funds
    ]

    for payment in payments:
        print(payment.process(accounts))
        print("-" * 40)

    for acc in accounts.values():
        print(acc)
```
