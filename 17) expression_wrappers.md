# 🧮 Django ORM: `ExpressionWrapper`

`ExpressionWrapper` is a powerful tool in Django ORM used to **wrap complex expressions** (especially involving calculations or type conversions) so they can be used inside `annotate()`, `aggregate()`, or `filter()` clauses.

---

## 🚀 What Is `ExpressionWrapper`?

`ExpressionWrapper` lets you:

- Perform calculations on model fields
- Specify the output field type (required for evaluation)
- Use arithmetic in ORM queries safely

---

## 🧾 Import

```python
from django.db.models import ExpressionWrapper, F, FloatField, DecimalField





✅ Example 1: Calculating Discounted Price


from django.db.models import F, DecimalField, ExpressionWrapper

Product.objects.annotate(
    discounted_price=ExpressionWrapper(
        F('price') * 0.9,
        output_field=DecimalField()
    )
)



✅ Example 2: Revenue per Order Item


from django.db.models import IntegerField

OrderItem.objects.annotate(
    revenue=ExpressionWrapper(
        F('quantity') * F('unit_price'),
        output_field=IntegerField()
    )
)


| Use Case                       | Example                                                |
| ------------------------------ | ------------------------------------------------------ |
| Perform math in `annotate()`   | `F('a') * F('b')`                                      |
| Apply arithmetic on `filter()` | `ExpressionWrapper(F('a') * F('b'), output_field=...)` |
| Control data type              | `output_field=FloatField()`                            |
| Complex conditions and logic   | Combined with `Case`, `When`, etc.                     |
