# 🔎 Django ORM Filtering Cheat Sheet

Filtering in Django ORM allows you to retrieve specific records from the database based on conditions. The `filter()` method is your best friend for querying data efficiently and expressively. 🛠️

---

## ✨ Basic Syntax

```python
Model.objects.filter(field_name=value)



---

## 📦 Basic Filters

| Filter            | Description                            | Example                                      |
|-------------------|----------------------------------------|----------------------------------------------|
| `exact`           | Matches the exact value                | `filter(name__exact='Pizza')`               |
| `iexact`          | Case-insensitive exact match           | `filter(name__iexact='pizza')`              |
| `contains`        | Checks if value is contained           | `filter(name__contains='ice')`              |
| `icontains`       | Case-insensitive contains              | `filter(name__icontains='Ice')`             |

---

## 🔢 Numeric Filters

| Filter    | Description                   | Example                     |
|-----------|-------------------------------|-----------------------------|
| `gt`      | Greater than                  | `filter(price__gt=100)`     |
| `gte`     | Greater than or equal to      | `filter(price__gte=100)`    |
| `lt`      | Less than                     | `filter(price__lt=100)`     |
| `lte`     | Less than or equal to         | `filter(price__lte=100)`    |
| `range`   | Between two values            | `filter(price__range=(50, 150))` |

---

## 🔡 Text Filters

| Filter         | Description                        | Example                          |
|----------------|------------------------------------|----------------------------------|
| `startswith`   | Starts with value                  | `filter(name__startswith='Chee')` |
| `istartswith`  | Case-insensitive starts with       | `filter(name__istartswith='chee')` |
| `endswith`     | Ends with value                    | `filter(name__endswith='cake')`   |
| `iendswith`    | Case-insensitive ends with         | `filter(name__iendswith='Cake')`  |

---

## 📅 Date & Null Filters

| Filter        | Description                         | Example                                 |
|---------------|-------------------------------------|-----------------------------------------|
| `date`        | Filters by exact date               | `filter(created_at__date='2025-07-01')` |
| `year`        | Filters by year                     | `filter(created_at__year=2025)`         |
| `month`       | Filters by month                    | `filter(created_at__month=7)`           |
| `day`         | Filters by day                      | `filter(created_at__day=2)`             |
| `isnull`      | Check for NULL values               | `filter(published_at__isnull=True)`     |

---

## 🧪 Others

| Filter     | Description                               | Example                            |
|------------|-------------------------------------------|------------------------------------|
| `in`       | Checks if value is in a list              | `filter(id__in=[1, 2, 3])`         |
| `regex`    | Matches regular expression                | `filter(name__regex=r'^[A-Z]')`    |
| `iregex`   | Case-insensitive regular expression       | `filter(name__iregex=r'^cake')`    |

---

> 📘 These filters make querying in Django ORM simple and expressive — no raw SQL required!