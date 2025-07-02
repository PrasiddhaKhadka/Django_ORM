# 🧠 Django ORM: Using `F()` Expressions

Django's `F()` expressions allow you to **reference model fields directly in queries**, enabling comparisons, updates, and arithmetic operations **without pulling data into Python** first. 🚀

---

## 📥 How to Import `F`

```python
from django.db.models import F


# Get products where stock is greater than sold
here stock itself is in database table and sold is another column in database table (evaluate two columns of databases)

Product.objects.filter(stock__gt=F('sold'))


stock__gt=F('sold') means: compare stock field to sold field.




🔗 Example: Comparing Fields
# Get all employees whose bonus is greater than their salary
Employee.objects.filter(bonus__gt=F('salary'))



➕ F() with Arithmetic
You can use F() with arithmetic operators:


# Give all employees a 10% raise
Employee.objects.update(salary=F('salary') * 1.10)
Other supported operations:

+ addition

- subtraction

* multiplication

/ division

% modulus

