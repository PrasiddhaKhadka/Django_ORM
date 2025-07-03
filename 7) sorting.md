# 🔃 Django ORM: Sorting Querysets

Sorting (also called **ordering**) is a common operation in Django ORM that allows you to control the **order in which results are returned** from the database.

---

## 🧱 Basic Syntax

Use the `.order_by()` method on any queryset:

```python
Model.objects.order_by('field_name')


## 📊 Sorting Methods in Django ORM

| Method                         | Description                          |
|--------------------------------|--------------------------------------|
| `.order_by('field')`           | Ascending order by field             |
| `.order_by('-field')`          | Descending order by field            |
| `.order_by('f1', '-f2')`       | Sort by `f1` ascending, then `f2` descending |
| `Meta.ordering = ['field']`    | Set default model-level sorting      |






📌 Tip: Default Ordering in Model


You can also define default ordering in your model using Meta:


class Product(models.Model):
    name = models.CharField(max_length=100)
    price = models.DecimalField(max_digits=6, decimal_places=2)

    class Meta:
        ordering = ['price'] 