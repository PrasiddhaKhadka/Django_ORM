# 🛠️ Django ORM: Creating Objects

In Django ORM, there are multiple ways to create and save records to the database. This guide covers the most commonly used methods to create objects in a clean and efficient way.

---

## 🧱 1. Using `.create()`

Creates and saves an object to the database in one step.

```python
Product.objects.create(name="iPhone", price=999.99)




✍️ 2. Creating an Instance Then .save()
Gives you full control before saving.

product = Product()
    product.name="MacBook"
    product.price=1999.99
    product.category = Category.objects.get(name="Electronics") || Category(pk=1) ||
product.save()
✅ Can modify fields or do logic before saving
✅ More flexible



3. Using get_or_create()
Gets an existing object or creates it if not found.


obj, created = Product.objects.get_or_create(
    name="AirPods",
    defaults={"price": 249.00}
)



🔁 4. Using update_or_create()
Gets an object and updates it, or creates it if it doesn’t exist.

obj, created = Product.objects.update_or_create(
    name="iPad",
    defaults={"price": 599.00}
)


| Method                | Creates Object | Updates Existing | Returns `(obj, created)` | Notes               |
| --------------------- | -------------- | ---------------- | ------------------------ | ------------------- |
| `.create()`           | ✅              | ❌                | ❌                        | Simple one-liner    |
| `.save()`             | ✅              | ✅ (on existing)  | ❌                        | Manual, flexible    |
| `.get_or_create()`    | ✅              | ❌                | ✅                        | Avoids duplicates   |
| `.update_or_create()` | ✅              | ✅                | ✅                        | Good for sync logic |
