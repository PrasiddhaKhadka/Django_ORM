# 🧮 Django ORM: `annotate()`

Django’s `annotate()` function is used to **add computed fields** (like counts, sums, or averages) to each object in a queryset. It’s commonly used when you want **aggregated values per object** rather than for the whole queryset.

---

## 📥 What is `annotate()`?

- `annotate()` works like `aggregate()` but on a **per-object** basis.
- It adds **extra fields** to each instance in the queryset.
- Often used with aggregate functions like `Count`, `Sum`, `Avg`, etc.

---

## 🧱 Basic Example

```python
from django.db.models import Count

# Count number of books written by each author
Author.objects.annotate(book_count=Count('book'))


## 📊 Comparison Table

| Query Type       | Example Result                                                                 |
|------------------|---------------------------------------------------------------------------------|
| **Without `annotate()`** | `[<Category: Electronics>, <Category: Books>, <Category: Clothing>]`       |
| **With `annotate(Avg)`** | `[<Category: Electronics (avg_price=299.99)>, <Category: Books (avg_price=15.50)>]` |


## ✅ Annotated Query Example

```python
from django.db.models import Avg

# Adds avg_price attribute to each category
Category.objects.annotate(avg_price=Avg('products__price'))