# 🚀 Django ORM: QuerySet Caching

Django QuerySets are **lazy** and **cache their results** after evaluation. Understanding how this caching works can help you write more efficient code and avoid unexpected database hits.

---

## 🧠 What Is QuerySet Caching?

- A Django QuerySet does **not hit the database** until it is evaluated (e.g., via `.all()`, `.filter()`, `.count()`, or iteration).
- Once evaluated, the results are **cached** in memory and reused on subsequent access.

---

## ✅ Example

```python
products = Product.objects.filter(is_active=True)

# First evaluation (triggers SQL query)
for product in products:
    print(product.name)

# Second evaluation (uses cache — no DB query)
for product in products:
    print(product.price)


🧪 Forcing Evaluation and Caching
You can force evaluation and caching using:


list(qs)
qs = list(qs) 




🧹 Clearing the Cache
You cannot clear a queryset cache once it is evaluated, but reassigning the queryset will give you a new one:

qs = Product.objects.all()
qs = Product.objects.none()




🍎📉 Performance Pitfall 📉🍎

# BAD: Triggers SQL twice
count = Product.objects.all().count()
first = Product.objects.all().first()

# GOOD: Reuse the queryset
qs = Product.objects.all()
count = qs.count()
first = qs.first()


| Scenario                       | Cache Used? |
| ------------------------------ | ----------- |
| Iterating twice on same var    | ✅ Yes       |
| Calling `.all()` twice         | ❌ No        |
| Slicing or chaining methods    | ❌ No        |
| Using `.values()` or `.only()` | ❌ No        |


✅ Best Practices
✅ Assign your queryset to a variable if used multiple times.

✅ Convert to list() if you need fixed data (e.g., in loops).

✅ Avoid calling .filter() or .all() multiple times on the same model.

⚠️ Be aware that .filter() and other methods return new querysets, not cached copies.