# 🧑‍💼 Django ORM Managers

In Django, **managers** are the interface through which database query operations are provided to Django models. Every model gets a default manager named `.objects`. But you can also define your **custom managers** to add custom query logic. 💡

---

## 📦 What is a Manager?

A manager is a class that manages database query operations for a model.

```python
# Using the default manager
foods = Food.objects.all() # objects is the manager here !! 
