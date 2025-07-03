# 🔄 Django ORM: Generic Relations

Django’s **Generic Relations** (also called **Generic Foreign Keys**) allow a model to create relationships to **any other model**. This is useful for building reusable components like comments, tags, likes, etc., that can be attached to multiple types of models.

---

## 🧠 What is a Generic Relation?

Normally, a `ForeignKey` must point to one specific model. But sometimes, you want to relate a model to **any model type dynamically** — that’s what `GenericForeignKey` is for.

Django uses three fields internally:

1. `content_type`: stores the model class (like `Blog`, `Product`)
2. `object_id`: stores the primary key of the related object
3. `GenericForeignKey`: a virtual field combining the two

---

## 📥 Import Requirements

```python
from django.contrib.contenttypes.models import ContentType
from django.contrib.contenttypes.fields import GenericForeignKey, GenericRelation



✅ Example: Comment Model That Can Attach to Any Object

from django.db import models
from django.contrib.contenttypes.fields import GenericForeignKey
from django.contrib.contenttypes.models import ContentType

class Comment(models.Model):
    content_type = models.ForeignKey(ContentType, on_delete=models.CASCADE)
    object_id = models.PositiveIntegerField()
    content_object = GenericForeignKey('content_type', 'object_id')

    text = models.TextField()
    created_at = models.DateTimeField(auto_now_add=True)


## Example to fetch

content_type= ContentType.objects.get_for_model(Product)

TaggedItem.objects.select_related('tag').filter(
    contenttype = content_type
    object_id = 1 (must be given dynamically!)
)