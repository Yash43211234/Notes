# Django (Full-Featured) Notes

# MVC Architecture in Django

Django follows **MTV (Model-Template-View)**, but conceptually aligns with **MVC**:

- **Model** → Handles data (database tables, business logic).  
- **View** → Contains business logic; interacts with Model and passes data to Templates.  
- **Template** → Handles presentation (HTML, CSS, JS).  
- **Controller** → Implicit; Django’s framework + URL dispatcher plays this role.  

---

## Request-Response Cycle

1. Client sends request → **URL Dispatcher**  
2. Mapped to **View**  
3. **View** interacts with **Model**  
4. Data passed to **Template**  
5. **Response** returned  

# Models & ORM (Object Relational Mapper)

- **Models** define the structure of database tables using Python classes.  
- Django’s **ORM (Object Relational Mapper)** allows interaction with the database using Python code instead of SQL.  

---

## Example

```python
from django.db import models

class Book(models.Model):
    title = models.CharField(max_length=100)
    author = models.CharField(max_length=100)
    published_date = models.DateField()


```
### Database Table

This will create a Book table in the database with columns:

- title → string (max length 100)
- author → string (max length 100)
- published_date → date



# Migrations & ORM Features

## Migrations
- **`makemigrations`** → Creates migration files based on model changes.  
- **`migrate`** → Applies those changes to the database.  

---

## ORM Features
- Provides **abstraction over SQL** → interact with the database using Python code.  
- Write queries using Python instead of raw SQL.  

---

## Example Queries

```python
# Fetch all records
Book.objects.all()  
# SQL → SELECT * FROM book;

# Filter records
Book.objects.filter(author="A")  
# SQL → SELECT * FROM book WHERE author="A";

# Fetch a single record
Book.objects.get(id=1)  
# SQL → SELECT * FROM book WHERE id=1;

# Create a new record
Book.objects.create(title="X", author="Y")  
# SQL → INSERT INTO book (title, author) VALUES ("X", "Y");
```

# Django REST Framework (DRF) for APIs

- **DRF** extends Django to build **RESTful APIs**.  

---

## Key Components

- **Serializers** → Convert complex data (e.g., QuerySets, Models) to **JSON** & vice versa.  
- **ViewSets** → Contain logic for **CRUD APIs**.  
- **Routers** → Automatically generate **URL patterns** for ViewSets.  

---

## Example: Serializer & ViewSet

```python
from rest_framework import serializers, viewsets
from .models import Book

# Serializer - converts model data to JSON
class BookSerializer(serializers.ModelSerializer):
    class Meta:
        model = Book
        fields = '__all__'

# ViewSet - provides CRUD operations
class BookViewSet(viewsets.ModelViewSet):
    queryset = Book.objects.all()
    serializer_class = BookSerializer
```

```python
from rest_framework.routers import DefaultRouter
from django.urls import path, include
from .views import BookViewSet

router = DefaultRouter()
router.register('books', BookViewSet)

urlpatterns = [
    path('', include(router.urls)),
]
```

✅ Now API endpoints like the following will be auto-generated:

- **GET** `/books/` → List all books  
- **POST** `/books/` → Create a book  
- **GET** `/books/{id}/` → Retrieve a book  
- **PUT** `/books/{id}/` → Update a book  
- **DELETE** `/books/{id}/` → Delete a book  

# Authentication, Admin Panel, Forms

---

## Authentication
- Built-in user system: **`django.contrib.auth`**  
- Features:  
  - Login / Logout  
  - Permissions  
  - Sessions  
- DRF adds:  
  - **Token Authentication**  
  - **JWT Authentication**  
  - **OAuth2**  

---

## Admin Panel
- Enabled by default at **`/admin/`**  
- Requires creating a **superuser** (`python manage.py createsuperuser`)  
- Register models to make them visible in the admin dashboard:  

```python
from django.contrib import admin
from .models import Book

admin.site.register(Book)
```
## Forms

- **Django Forms** → Provide **server-side validation** and rendering of HTML form fields.  

### Example: Basic Form

```python
from django import forms

class BookForm(forms.Form):
    title = forms.CharField(max_length=100)
```

### Example: ModelForm  
- **ModelForms** → Auto-generate form fields directly from models.  

```python
from django.forms import ModelForm
from .models import Book

class BookForm(ModelForm):
    class Meta:
        model = Book
        fields = ['title', 'author']
```

# Deployment Basics

## a) Heroku

### Steps:
1. Install **Heroku CLI**  
2. Create a **Procfile** in project root:  
   ```txt
   web: gunicorn projectname.wsgi
### Install Required Packages
- `gunicorn`  
- `dj-database-url`  
- `whitenoise`  

---

### Initialize Git Repo & Push to Heroku
```bash
git init
heroku create
git add .
git commit -m "Deploy"
git push heroku main
```

## b) AWS (Elastic Beanstalk / EC2)

- Use **Elastic Beanstalk** for easy deployment.  
- Configure **environment variables** for DB, secret key, etc.  
- Use **S3** for static and media file storage.  

---

## c) Render

- Simple cloud hosting similar to Heroku.  

### Steps:
1. Connect **GitHub repo**  
2. Configure:  
   ```txt
   gunicorn projectname.wsgi

# ✅ Key Takeaways

- **Django is MTV** (like MVC).  
- **Models + ORM** = Database abstraction.  
- **DRF** = Easy API creation.  
- Built-in **Authentication & Admin** = Powerful for rapid development.  
- **Deployment** = `gunicorn` + cloud provider (Heroku / AWS / Render).  

