# 📦 Django ORM: `prefetch_related`

In Django ORM, `prefetch_related()` is used to optimize **Many-to-Many** and **reverse ForeignKey** relationships by reducing the number of queries needed to fetch related data.

---

## 🚀 What is `prefetch_related()`?

`prefetch_related()` performs a separate query for each related object and does a **Python-level join** — combining the results in memory.

It’s ideal for:
- `ManyToManyField`
- Reverse `ForeignKey` relationships
- Deep nested relations

---

## 🧠 When to Use It

- When you're accessing **many-to-many** fields.
- When you're accessing a model’s **reverse foreign key** (e.g., `author.book_set.all()`).
- To avoid **N+1 query issues** in these cases.

---

## ⚡ Without `prefetch_related()`

```python
# Looping over authors and their books
for author in Author.objects.all():
    for book in author.book_set.all():  # ❌ Triggers a new query for each author
        print(book.title)



✅ With prefetch_related()
# Optimized version
authors = Author.objects.prefetch_related('book_set')
for author in authors:
    for book in author.book_set.all():  # ✅ No extra DB hits
        print(book.title)



🔗 Multiple Relationships
You can prefetch multiple related fields:

Author.objects.prefetch_related('book_set', 'profile__awards')
