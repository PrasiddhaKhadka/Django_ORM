# 🔍 Retrieving Data in Django ORM

In Django ORM, you retrieve data from the database using **querysets**. A queryset represents a collection of objects from your database. 🗃️

Here are the most common methods used to retrieve data:

---

## 📃 `all()`

Returns **all records** in the table.

```python
from myapp.models import Food

foods = Food.objects.all()


## 📃 `get()`
Returns a single object that matches the query. If none or more than one object is found, it raises an error.

food = Food.objects.get(id=1)


⚠️ Throws:

DoesNotExist if no match

MultipleObjectsReturned if more than one match



🔍 filter()
Returns a queryset of all objects that match the given filter.

cheap_foods = Food.objects.filter(price__lt=10)


# 📘 Django ORM: QuerySet Retrieval Methods

Django ORM provides a variety of powerful and easy-to-use methods for retrieving data from the database. Below is a handy reference table for commonly used queryset methods.

---

## 🔍 Retrieval Methods Overview

| Method           | Description                    |
| ---------------- | ------------------------------ |
| `.all()`         | Returns all objects            |
| `.get()`         | Returns a single object        |
| `.filter()`      | Filters and returns a queryset |
| `.exclude()`     | Excludes matching objects      |
| `.first()`       | First item from the queryset   |
| `.last()`        | Last item from the queryset    |
| `.count()`       | Number of matching records     |
| `.exists()`      | Checks if records exist        |
| `.order_by()`    | Orders records                 |
| `.values()`      | Dictionary-style queryset      |
| `.values_list()` | Tuple-style queryset           |
| `.distinct()`    | Removes duplicates             |

---

## 🧠 Tips

- Use `.filter()` when you're expecting **multiple results**
- Use `.get()` only if you're sure the query returns a **single object**
- Always handle exceptions like `DoesNotExist` and `MultipleObjectsReturned` with `.get()`
- Use `.exists()` to **optimize** queries where you only need to check for presence

---

> 📌 Mastering these methods will help you write cleaner, faster, and more efficient Django applications.