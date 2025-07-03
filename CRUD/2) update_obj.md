# 🔄 Django ORM: Updating Objects

Django provides several ways to update records in the database using its ORM. This guide covers all the common techniques — from updating a single record to bulk updates.

---

## ✍️ 1. Update Using `.save()`

Used when you retrieve an object, change fields, and save it.

```python
product = Product.objects.get(id=1) (!! 🍎🍎🍎🍎.get garena vani jun value naya cha tyo matra update huncha baki sabai null wa empty vaidincha !! 🍎🍎🍎🍎)
product.name = "iPhone 15"
product.price = 1299.00
product.save()

✅ Easy to use
✅ Triggers model signals (pre_save, post_save)
❌ Not efficient for bulk updates




⚡ 2. Bulk Update Using .update()
Updates multiple records at once without fetching them⚡

Product.objects.filter(category__name="Electronics").update(discount=10)

✅ Very fast (single SQL query)
❌ Does not trigger model signals
❌ Does not call save() or field validation




🔁 3. Using update_or_create()
Updates a record if it exists, or creates a new one

obj, created = Product.objects.update_or_create(
    name="AirPods",
    defaults={"price": 229.00}
)

obj: The object that was updated or created

created: True if a new object was created

✅ Convenient for syncing and upserts
✅ Triggers save signals



| Method               | Triggers `.save()` | Triggers Signals | Suitable for Bulk |
| -------------------- | ------------------ | ---------------- | ----------------- |
| `.save()`            | ✅                  | ✅                | ❌                 |
| `.update()`          | ❌                  | ❌                | ✅                 |
| `update_or_create()` | ✅                  | ✅                | ❌                 |
