# 🔗 Django ORM: `select_related`

In Django ORM, `select_related` is used to optimize database queries involving **foreign key** or **one-to-one** relationships by performing a **SQL join** and retrieving related objects in a **single query**.

---

## 🚀 What Does `select_related` Do?

When you access a related object (e.g., `order.customer.name`), Django normally performs an additional query.

With `select_related`, Django performs a **single JOIN query**, avoiding the extra database hit.

---

## 📥 Syntax

```python
# Syntax: Use inside queryset
Order.objects.select_related('customer')



⚡ Performance Without select_related

orders = Order.objects.all()
for order in orders:
    print(order.customer.name)  # ⚠️ Triggers an extra query per order




✅ Performance With select_related
orders = Order.objects.select_related('customer')
for order in orders:
    print(order.customer.name)  # ✅ No extra queries



.

🧠 When to Use
    Use when you're accessing ForeignKey or OneToOneField data repeatedly.

    Avoid for ManyToMany relationships — use prefetch_related instead. ///. ALSO USE PREFETCH FOR REVERSE RELATION CASES !

    Best in list views or APIs where related data is displayed.




😁😎 Multiple Levels (Chained Relationships)

You can follow relationships across models using double underscores (__):

Order.objects.select_related('customer__profile')


| Feature             | Description                                     |
|---------------------|-------------------------------------------------|
| `.select_related()` | Optimizes ForeignKey and OneToOne relations     |
| Type                | SQL JOIN (single query)                         |
| Use case            | Avoid N+1 queries when accessing related fields |
| Not for             | ManyToMany fields (use `prefetch_related`)      |
