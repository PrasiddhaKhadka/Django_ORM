# 📊 Django ORM: Grouping Data with `.values()` and `.annotate()`

In Django ORM, **grouping** is achieved using a combination of `.values()` and `.annotate()`. This mimics the SQL `GROUP BY` clause, allowing you to perform aggregations on grouped data.

---

## 🔍 What is Grouping?

Grouping lets you summarize or aggregate data **based on distinct field values** — e.g., total orders per customer, average price per category, etc.

---

## 🧠 How Grouping Works in Django

- `.values('field')` specifies the field to group by.
- `.annotate()` applies an aggregation (e.g., `Count`, `Sum`, `Avg`) to each group.

---

## ✅ Example: Total Products per Category

```python
from django.db.models import Count

Product.objects.values('category__name').annotate(total=Count('id'))



📦 Output:

[
  {'category__name': 'Electronics', 'total': 50},
  {'category__name': 'Books', 'total': 20},
]

