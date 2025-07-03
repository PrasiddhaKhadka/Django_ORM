# 💤 Deferring Fields in Django ORM

In Django ORM, you can **defer the loading of certain fields** when querying your models using `.only()` and `.defer()`. This improves performance by reducing the amount of data retrieved from the database — especially helpful for large models.

---

## 🎯 Why Defer Fields?

- Reduce memory usage.
- Improve query performance.
- Avoid loading large fields (e.g., image, text) when not needed.

---

## ✅ `.only()` – Load Only Specific Fields

Returns full model instances but **only retrieves the specified fields immediately**. Other fields are deferred until accessed.

```python
# Load only 'name' and 'price' fields
Product.objects.only('name', 'price')




⚠️ Flaws and Caveats of .only()

# This will trigger a new query for each object's description
products = Product.objects.only('name')
for p in products:
    print(p.description) 

This creates an N+1 query problem, especially dangerous inside loops.





---

## 🆚 Comparison: `.only()` vs `.defer()`

| Method     | Loads Immediately        | Deferred Fields    |
|------------|--------------------------|--------------------|
| `.only()`  | Only listed fields       | All others         |
| `.defer()` | All fields except listed | Only listed fields |

---



## 💡 Examples

### ✅ Using `.only()`

```python
# Only load 'id' and 'name'; other fields like 'description' are deferred
products = Product.objects.only('id', 'name')

for product in products:
    print(product.name)         # ✅ No extra query
    print(product.description)  # ⚠️ Triggers extra query per object (Loop if 100 times then 100 times will be called!!)





✅ Using .defer()

# Load all fields except 'description'
products = Product.objects.defer('description')

for product in products:
    print(product.name)         # ✅ No extra query
    print(product.description)  # ⚠️ Triggers extra query per object





