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
user.id #database primary-key id

#Django provides many api for database lookup
User.objects.all() #list of user
User.objects.get(id=1) #user with id 1
User.objects.get(name__statswith='madan')

#Django also handles the relational lookup
userPost = user.post #gets post related user
post.body #gets body field of post

#we can also deeply nest the query
Post.objects.filter(user__name__startswith='madan') #gets post by user whose name starts with "madan"

user.delete() #deletes the user
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

### Mapping URLs

In Django we can specify config to map URL to a callback.

The parameter tags `<>` are used to capture values from URL.

Django search from top to bottom for matching URL, once the match is found, it stops and call the callback. 

The callback function gets a request object \(request metadata\) and the values captured in the pattern. `callback(request, name=madan)` 

The convention is put callback function inside `views.py` 

{% code-tabs %}
{% code-tabs-item title="app/post/urls.py" %}
```python
from django.urls import path, url

urlpatterns = [
    path('post/<int:pk>/', views.post),
    path('post/<string:title>/', views.post_title),
]

#we can also use regex and name the route for later use
urlpatterns = [
    url(r'^post/$', views.post_title, name=unique_route_name)
]

```
{% endcode-tabs-item %}
{% endcode-tabs %}

```python
#use case for unique url name
from django.core.urlresolvers 
from django.http import HttpResponseRedirect
    
#eg, we can use name of route to create a HttpResponseRedirect
def redirect_to_title(request):
    title = post_title
    return HttpResponseRedirect(reverse('unique_route_name', args=(title,)))  
    
```

view/callback are responsible for returning an `HttpResponse` object with request page contents or `Http404` on error.

{% code-tabs %}
{% code-tabs-item title="app/post/views.py" %}
```python
from django.shortcuts import render
from .models import Post

def post_title(request, title):
    #get posts with this title
    posts_list = Post.objects.filter(title__startswith=title)
    
    #put it into collection to be used in template
    context = {'title': title, 'posts_list': posts_list}
    
    #pass the request, context to template
    return render(request, 'post/title.html', context)
    
```
{% endcode-tabs-item %}
{% endcode-tabs %}

### Template

Django project can be configured with one or several template engines. 

Django defines a standard API for loading and rendering templates regardless of the backend. 

Django template language \(DTL\) is django's own template system.

Templates engines are configured with `TEMPLATES` setting, one for each engine. 

```python
TEMPLATES = [
    {
        'BACKEND': 'django.template.backends.django.DjangoTemplate'
        'DIRS': []
        'APP_DIRS': True,
        'OPTIONS': {},
    },
]

```

* `BACKEND` dotted path to template engine class implementing Django's template backend API. 
* `DIRS` list of directories for engines to look template in
* `APP_DIRS` should look for templates inside installed applications
* `OPTIONS` backend-specific settings

#### Template syntax

variables surrounded by double-curly braces `{{ post.titl }}` . Can use filter by piping variables `{{ post.date|date:"F j, Y" }}` . can write custom template filters and template tags. Also has template inheritance feature \`{% extends "base.html" %} \( loads base blocks and fills the blocks with following templates \) 

{% code-tabs %}
{% code-tabs-item title="app/post/templates/post/title.html" %}
```python
{% extends "base.html" %}

{% block title %}Posts with titile: {{ title }}{% endblock %}

{% block content %}
<h4>Posts title is {{ title }}</h4>
{% endblock %}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

{% code-tabs %}
{% code-tabs-item title="app/templates/base.html" %}
```python
{% load static %}
<html>
<head>
</head>
<body>
{% block content %}{% block %}
</body>
</html>
```
{% endcode-tabs-item %}
{% endcode-tabs %}

#### Helpful links

* [Models doc](https://docs.djangoproject.com/en/2.2/topics/db/models/)
* [Making queries](https://docs.djangoproject.com/en/2.2/topics/db/queries/)
* [URLs](https://docs.djangoproject.com/en/2.2/topics/http/urls/)
* [Templates](https://docs.djangoproject.com/en/2.2/topics/templates/)

