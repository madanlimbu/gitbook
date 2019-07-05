---
description: Django quick notes
---

# Overview

### Model

Django comes with an Object relational mapper \(ORM\) to describe and manipulate with data.

Model are subclass of `django.db.models.Model` 

```python
from django.db import models

class User(models.Model):
    name = models.CharField(max_length=70)
    
class Post(models.Model):
    title = models.CharField(max_length=70)
    body = models.TextField(blank=True)
    user = models.ForeignKey(User, on_delete=models.CASCADE)
    
    def __str__(self):
        return self.title
```

Django also provide database-access API. 

Model represents a Database-table and a record/row in table represents an instance of that model.

{% code-tabs %}
{% code-tabs-item title="app/post/db.py" %}
```python
from .models import User

user = User(name='madan') #instance of User
user.save() #insert to database
```
{% endcode-tabs-item %}
{% endcode-tabs %}

### Migrations

In Django, Migrations is a way of propagating changes from models to database schema.

The migration files for each app lives in a `migration` directory.

```python
#Most used cli to interact with migration

#stages/create new migration based on changes to model
python manage.py makemigrations

#or give a meaningful name to migraiton file
python manage.py makemigrations --name GOODNAME APPNAME

#apply changes from migrations
python manage.py migrate

#lists projects migraitons and their status
python manage.py showmigrations

#display SQL statemetns for the specific migration
python manage.py sqlmigrate PROJECT_NAME MIGRATION

```

#### Helpful links

* [Models doc](https://docs.djangoproject.com/en/2.2/topics/db/models/)
* [Making queries](https://docs.djangoproject.com/en/2.2/topics/db/queries/)
* 
