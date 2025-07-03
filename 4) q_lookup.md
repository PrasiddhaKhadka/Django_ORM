# 🧠 Django ORM: Q Lookup (Complex Queries)

The `Q` object in Django ORM is used to create **complex queries** with **OR**, **AND**, and **NOT** conditions that go beyond the default `filter()` behavior.

---

## 📥 How to Import Q

```python
from django.db.models import Q


## 🤔 Why Use `Q`?

Normally, `filter()` combines conditions using **AND** logic:

```python
# Both conditions must be true (AND)
Product.objects.filter(category='Snacks', price__lt=20)



## Using Q for OR Conditions

    Find products that are either cheap OR belong to Snacks
Product.objects.filter(Q(price__lt=10) | Q(category='Snacks'))



#  Using Q for AND Conditions

Product.objects.filter(Q(category='Drinks') & Q(price__lt=5))



❌ Negating Conditions with ~Q

Product.objects.filter(~Q(category='Junk'))




🔍 Real-World Examples
# Users whose name starts with A or email ends with .edu
User.objects.filter(Q(name__istartswith='a') | Q(email__iendswith='.edu'))

# Orders placed in 2025 and not yet delivered
Order.objects.filter(Q(date__year=2025) & ~Q(status='delivered'))