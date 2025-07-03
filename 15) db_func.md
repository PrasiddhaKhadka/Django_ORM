# 🛠️ Django ORM: Database Functions (`django.db.models.functions`)

Django provides a rich set of **database functions** that allow you to manipulate or transform values directly within ORM queries — similar to SQL functions.

These are available in:
```python
from django.db.models.functions import *


# 📋 Django ORM Database Functions — Cheat Sheet

---

## 🔡 String Functions

| Function   | Description                          | Example                                                            |
|------------|--------------------------------------|--------------------------------------------------------------------|
| `Lower()`  | Converts a string field to lowercase | `annotate(lower_name=Lower('name'))`                               |
| `Upper()`  | Converts a string field to uppercase | `annotate(upper_name=Upper('name'))`                               |
| `Length()` | Returns the length of a string       | `annotate(name_length=Length('name'))`                             |
| `Concat()` | Concatenates multiple fields         | `annotate(full_name=Concat('first_name', Value(' '), 'last_name'))`|
| `Substr()` | Extracts part of a string            | `annotate(short_name=Substr('name', 1, 3))`                         |
| `Trim()`   | Removes whitespace                   | `annotate(trimmed_name=Trim('name'))`                              |

---

## 📅 Date & Time Functions

| Function     | Description                                | Example                                                |
|--------------|--------------------------------------------|--------------------------------------------------------|
| `Now()`      | Current timestamp                          | `filter(created_at__lte=Now())`                        |
| `Extract()`  | Extract part of a date (e.g., year/month)  | `annotate(year=ExtractYear('created_at'))`             |
| `Trunc()`    | Truncate date/time to a specific unit      | `annotate(date=TruncDay('created_at'))`                |

---

## 🔢 Math Functions

| Function   | Description            | Example                                    |
|------------|------------------------|--------------------------------------------|
| `Abs()`    | Absolute value         | `annotate(diff=Abs(F('stock') - 10))`      |
| `Round()`  | Round to nearest int   | `annotate(rounded_price=Round('price'))`   |
| `Ceil()`   | Round up               | `annotate(ceil_price=Ceil('price'))`       |
| `Floor()`  | Round down             | `annotate(floor_price=Floor('price'))`     |
| `Sqrt()`   | Square root            | `annotate(sqrt_value=Sqrt('quantity'))`    |

---

## 🧠 Conditional Functions

| Function      | Description                          | Example                                                          |
|---------------|--------------------------------------|------------------------------------------------------------------|
| `Coalesce()`  | Returns the first non-null value     | `annotate(name_or_fallback=Coalesce('name', Value('N/A')))`      |
| `NullIf()`    | Returns NULL if two values are equal | `annotate(is_null=NullIf('status', 'inactive'))`                 |
