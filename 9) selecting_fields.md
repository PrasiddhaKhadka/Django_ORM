# 🎯 Selecting Specific Fields in Django ORM Queries

By default, Django ORM returns full model instances when querying the database. Sometimes, you only need specific fields to improve performance or simplify data handling.

---

## ⚡ Methods to Select Specific Fields

### 1. `.values()`

Returns a queryset of dictionaries — each dictionary contains only the specified fields.

```python
# Return only 'id' and 'name' fields for all products
Product.objects.values('id', 'name')



## output
[
  {'id': 1, 'name': 'Chocolate'},
  {'id': 2, 'name': 'Vanilla'},
]



2. .values_list()

Product.objects.values_list('id', 'name')

output:
[
  (1, 'Chocolate'),
  (2, 'Vanilla'),
]


Product.objects.values_list('name', flat=True)
Output: ['Chocolate', 'Vanilla']


3. .only()

Returns full model instances but loads only the specified fields from the database.

# Load only 'name' and 'price' fields for all products
Product.objects.only('name', 'price')



| Method           | Returns                     | Use Case                                              |
| ---------------- | --------------------------- | ----------------------------------------------------- |
| `.values()`      | Dicts (no model instances)  | When you want lightweight data without model methods  |
| `.values_list()` | Tuples (no model instances) | When you want simple tuples or flat lists             |
| `.only()`        | Model instances             | When you want models but want to defer loading fields |
