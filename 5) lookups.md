# 🔍 Django ORM Lookups Explained

In Django, **lookups** are special keywords used in query expressions to filter and retrieve specific data from the database. They are used inside methods like `.filter()`, `.exclude()`, `.get()`, etc.

---

## 🧱 Basic Syntax

```python
Model.objects.filter(field__lookup=value)


Product.objects.filter(price__gt=100)

price = field
gt = lookup
100 = value to compare


## 🔗 Relationship Lookups (Very Important!)

One of the most **powerful and important concepts** in Django ORM is the ability to perform lookups across **related models** using the **double underscore (`__`)** syntax.

This allows you to filter data not just by fields on the current model, but also by fields on **related models** (via `ForeignKey`, `OneToOneField`, or `ManyToManyField`).

### 🧠 Example

```python
# Get all orders where the customer's email contains 'gmail'
Order.objects.filter(customer__email__icontains='gmail')