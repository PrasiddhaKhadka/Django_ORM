# 🔢 Django ORM: Limiting Querysets

In Django ORM, **limiting** allows you to control **how many records** are returned from a query — just like SQL’s `LIMIT` and `OFFSET`.

---

## ✂️ Slicing Querysets

You can use **Python-style slicing** to limit results:

```python
# Get first 5 records
Product.objects.all()[:5]

# Get records 6 to 10
Product.objects.all()[5:10]




🚫 No Negative Indexing

Django does not support negative indexing like [-1]:

Product.objects.all()[-1]

Instead,

Product.objects.all().last()


## 🔢 Common Methods to Limit Querysets in Django ORM

| Method                 | Purpose                        |
|------------------------|-------------------------------|
| `[:n]`                 | Limit to first `n` records     |
| `[start:end]`          | Offset and limit slice         |
| `.first()` / `.last()` | Return first or last object    |
| `.exists()`            | Check if any records exist     |
| `.count()`             | Return total number of records |
