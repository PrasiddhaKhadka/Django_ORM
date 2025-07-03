# 🗑️ Django ORM: Deleting Objects

Django provides powerful tools to delete database records through the ORM. This guide explains different ways to delete single or multiple objects, and considerations around cascading and soft deletes.

---

## ❌ 1. Deleting a Single Object

You can delete a single object by calling its `.delete()` method.

```python
product = Product.objects.get(id=1)
product.delete()


✅ Triggers pre_delete and post_delete signals
❌ Object is removed permanently from the database



🔁 2. Bulk Delete Using QuerySets
You can delete multiple objects at once using QuerySet.delete():

Product.objects.filter(discontinued=True).delete()




🧲 3. Cascading Deletes
If a model has a ForeignKey or OneToOneField with on_delete=models.CASCADE, deleting a parent will also delete related objects.

class Order(models.Model):
    ...

class OrderItem(models.Model):
    order = models.ForeignKey(Order, on_delete=models.CASCADE)




🧼 4. Soft Deletes (Recommended for Audit/Recovery)
Instead of actually deleting records, mark them as inactive:

class Product(models.Model):
    name = models.CharField(max_length=100)
    is_deleted = models.BooleanField(default=False)

# Soft delete
product = Product.objects.get(id=1)
product.is_deleted = True
product.save()
Then filter active records:

Product.objects.filter(is_deleted=False)



| Method                     | Deletes Data | Triggers Signals | Efficient | Notes                                   |
| -------------------------- | ------------ | ---------------- | --------- | --------------------------------------- |
| `.delete()` on instance    | ✅            | ✅                | ❌         | Good for single object w/ signals       |
| `QuerySet.delete()`        | ✅            | ❌                | ✅         | Fast bulk delete, no per-instance logic |
| `on_delete=models.CASCADE` | ✅            | ✅                | ✅         | Deletes related objects                 |
| Soft delete (custom flag)  | ❌            | ✅ (manual save)  | ✅         | Safer and reversible                    |

