# 🧮 Django ORM: Aggregating Objects

Aggregation is the process of **computing summary values** (like totals, averages, counts) from a queryset. Django provides an intuitive way to do this using the `aggregate()` and `annotate()` methods along with built-in aggregate functions.

---

## 📦 Importing Aggregate Functions

Before using aggregations, import the required functions from `django.db.models`:

```python
from django.db.models import Count, Sum, Avg, Max, Min



✅ Examples:

# Total price of all products
Product.objects.aggregate(total=Sum('price'))

# Average product price
Product.objects.aggregate(average=Avg('price'))

# Maximum price
Product.objects.aggregate(max_price=Max('price'))

# Count of all products
Product.objects.aggregate(count=Count('id'))



Output: 

{'total': 6500}
{'average': 1300.0}
{'max_price': 2000}
{'count': 5}
