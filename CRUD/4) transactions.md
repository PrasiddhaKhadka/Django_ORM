# 💳 Django ORM: Transactions

A **transaction** in Django ensures that a group of database operations is treated as a **single unit of work** — either all operations succeed, or none are applied. This prevents partial updates and maintains **data integrity**.

---

## 🔐 What is a Transaction?

- A **transaction** wraps one or more operations so they **succeed or fail together**.
- If any operation inside the block fails, all changes are **rolled back**.

---

## ✅ Using `@transaction.atomic`

Django provides the `transaction.atomic` decorator/context manager to manage transactions.

### 🔸 Decorator Example

```python
from django.db import transaction

@transaction.atomic
def create_order():
    order = Order.objects.create(...)
    OrderItem.objects.create(order=order, ...)
    Payment.objects.create(order=order, ...)




🔸 Context Manager Example

from django.db import transaction

def process_payment():
    with transaction.atomic():
        user.balance -= 100
        user.save()
        log_payment(user)




🧨 Rollbacks on Exceptions
If an exception is raised within the atomic block, everything is rolled back automatically.

from django.db import transaction

def transfer_funds(a, b, amount):
    with transaction.atomic():
        a.balance -= amount
        a.save()
        
        # Simulate error
        if amount > 1000:
            raise ValueError("Transfer limit exceeded")
        
        b.balance += amount
        b.save()



| Use Case                   | Why                          |
| -------------------------- | ---------------------------- |
| Bank transfers             | Ensures both accounts update |
| E-commerce checkout        | Avoids double billing/orders |
| Multi-step object creation | Avoids half-created entities |
| Any critical DB operation  | Guarantees consistency       |





| Tool / Method               | Purpose                                     |
| --------------------------- | ------------------------------------------- |
| `@transaction.atomic`       | Decorator for function-level transaction    |
| `with transaction.atomic()` | Block-level transaction context             |
| Automatic rollback          | Any uncaught exception triggers rollback    |
| Savepoints                  | Rollback partial block inside a transaction |






⚠️ Savepoints (Nested Transactions)
Django creates savepoints inside nested atomic blocks. You can roll back only part of the transaction if needed.


with transaction.atomic():
    do_important_things()
    
    try:
        with transaction.atomic():
            risky_operation()
    except:
        # Rolls back only the nested block
        log_error("risky_operation failed")