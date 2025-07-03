# 🧰 Django ORM: Custom Managers

In Django, **Managers** are the interface through which database query operations are provided to Django models. A **custom manager** allows you to encapsulate **common or complex query logic** and make your code more readable and reusable.

---

## 🧠 What Is a Custom Manager?

A custom manager is a subclass of `models.Manager` with extra methods or query filters specific to your app’s needs.

---

## 🔧 Creating a Custom Manager

```python
from django.db import models

class ActiveManager(models.Manager):
    def get_queryset(self):
        return super().get_queryset().filter(is_active=True)

    def featured(self):
        return self.get_queryset().filter(is_featured=True)



## EXAMPLES:
class TaggedItemCustomManager(models.Manager):

    def get_tags_for(self,model,obj_id):
        content_type = ContentTypes.model.get_for_model(model)
       return TaggedItems.object.select_related('tag').filter(content_type = content_type, object_id = obj_id)



class Tagged(models.Model):
    object = TaggedItemCustomManager() # (refrencing the model)
    content_type = models.Foreignkey(CONTENTTYPE, on_delete=models.CASCADE) 
    object_id = models.PostivieIntegerField()
    content_object = GenericForeignKey(content_type, object_id)


@@ CALLING THE MANAGER:

    😎 😎 😎  TaggedItem.objects.get_tags_for(Product,1) 😎 😎 😎 

    