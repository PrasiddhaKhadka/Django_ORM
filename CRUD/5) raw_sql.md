# 🧾 Django ORM: Raw SQL Queries

While Django ORM is powerful and expressive, there are times when you may need to write raw SQL — for performance, complex joins, database-specific features, or legacy queries. Django supports raw SQL via two main approaches.

---

## 🧠 When to Use Raw SQL

✅ Complex queries not supported by ORM  
✅ Performance tuning with optimized SQL  
✅ Interacting with views or stored procedures  
✅ Raw access for reporting or analytics  

❌ Not recommended for simple CRUD — prefer Django ORM for portability and security

---

## 1️⃣ Using `.raw()` for Read-Only Queries

The `raw()` method lets you run raw **SELECT** queries and map the results to model instances.

```python
# Basic usage
Product.objects.raw("SELECT * FROM store_product WHERE price > %s", [500])

✅ Parameters are safely escaped
✅ Returns model instances
❌ Only works with SELECT





🧪 Example: Custom Field Selection

queryset = Product.objects.raw("""
    SELECT id, name, price
    FROM store_product
    WHERE is_active = true
""")

for product in queryset:
    print(product.name, product.price)
