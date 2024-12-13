Here's a **comprehensive Django handbook** that covers all key concepts, commands, and structures for working with Django, the powerful Python web framework.

---

# **Django Handbook**

## **1. Installation and Setup**

### **Install Django**
```bash
# Install Django
pip install django

# Verify installation
django-admin --version
```

### **Create a Django Project**
```bash
# Start a new project
django-admin startproject project_name

# Navigate into project directory
cd project_name

# Run the development server
python manage.py runserver
```
Access the app at `http://127.0.0.1:8000`.

---

## **2. Project Structure**

### **Basic Project Structure**
```
project_name/
│
├── manage.py                # Command-line utility
├── project_name/
│   ├── __init__.py          # Treats directory as a package
│   ├── settings.py          # Configuration file
│   ├── urls.py              # URL routing
│   ├── asgi.py              # ASGI config for async servers
│   └── wsgi.py              # WSGI config for production
│
└── app_name/                # Apps created within the project
    ├── admin.py             # Admin interface
    ├── apps.py              # App configuration
    ├── models.py            # Database models
    ├── views.py             # Application views
    ├── tests.py             # Unit tests
    ├── urls.py              # URL routing for app
    ├── migrations/          # Database migrations
    └── templates/           # HTML templates
```

---

## **3. Creating a Django App**
Django projects are divided into reusable **apps**.

### **Create an App**
```bash
python manage.py startapp app_name
```

### **Register the App**
Add your app to the `INSTALLED_APPS` in `settings.py`:
```python
INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    'app_name',  # Add your app here
]
```

---

## **4. Views**

Views handle logic and return HTTP responses.

### **Basic View**
```python
from django.http import HttpResponse

def home(request):
    return HttpResponse("Hello, Django!")
```

### **Class-Based View**
```python
from django.views import View
from django.http import HttpResponse

class HomeView(View):
    def get(self, request):
        return HttpResponse("Hello from Class-Based View!")
```

---

## **5. URLs**

### **URL Configuration**
**project_name/urls.py**
```python
from django.contrib import admin
from django.urls import path, include

urlpatterns = [
    path('admin/', admin.site.urls),
    path('', include('app_name.urls')),  # Include app URLs
]
```

**app_name/urls.py**
```python
from django.urls import path
from . import views

urlpatterns = [
    path('', views.home, name='home'),  # Route to home view
]
```

---

## **6. Templates**

### **Setup Templates**
In `settings.py`, configure the `TEMPLATES` directory:
```python
TEMPLATES = [
    {
        'DIRS': [BASE_DIR / 'templates'],  # Add template directory
    },
]
```

### **Folder Structure**
```
project_name/
    templates/
        app_name/
            index.html
```

### **Render a Template**
**views.py**
```python
from django.shortcuts import render

def home(request):
    return render(request, 'app_name/index.html', {'name': 'Django'})
```

**templates/app_name/index.html**
```html
<!DOCTYPE html>
<html>
<body>
    <h1>Hello, {{ name }}!</h1>
</body>
</html>
```

---

## **7. Models**

### **Define a Model**
**models.py**
```python
from django.db import models

class Book(models.Model):
    title = models.CharField(max_length=100)
    author = models.CharField(max_length=50)
    published_date = models.DateField()

    def __str__(self):
        return self.title
```

### **Run Migrations**
```bash
# Create migration files
python manage.py makemigrations

# Apply migrations to the database
python manage.py migrate
```

### **Django Shell**
Interact with the database using the shell:
```bash
python manage.py shell
```

**Example:**
```python
from app_name.models import Book
Book.objects.create(title="Django Handbook", author="John", published_date="2024-06-01")
books = Book.objects.all()
print(books)
```

---

## **8. Admin Interface**

### **Enable Admin**
Register models in **admin.py**:
```python
from django.contrib import admin
from .models import Book

admin.site.register(Book)
```

### **Access Admin Panel**
1. Create a superuser:
    ```bash
    python manage.py createsuperuser
    ```
2. Access the admin at `http://127.0.0.1:8000/admin/`.

---

## **9. Forms**

### **Django Forms**
**forms.py**
```python
from django import forms

class BookForm(forms.Form):
    title = forms.CharField(max_length=100)
    author = forms.CharField(max_length=50)
```

### **Use Forms in Views**
```python
from .forms import BookForm

def book_view(request):
    form = BookForm()
    return render(request, 'app_name/book_form.html', {'form': form})
```

**book_form.html**
```html
<form method="post">
    {% csrf_token %}
    {{ form.as_p }}
    <button type="submit">Submit</button>
</form>
```

---

## **10. Static Files**

### **Folder Structure**
```
static/
    css/
        style.css
```

### **Settings Configuration**
Add to `settings.py`:
```python
STATIC_URL = '/static/'
STATICFILES_DIRS = [BASE_DIR / "static"]
```

### **Load Static Files in Templates**
```html
{% load static %}
<link rel="stylesheet" href="{% static 'css/style.css' %}">
```

---

## **11. Middleware**

Middleware processes requests/responses globally.

**Example Custom Middleware**:
```python
class SimpleMiddleware:
    def __init__(self, get_response):
        self.get_response = get_response

    def __call__(self, request):
        print("Before view")
        response = self.get_response(request)
        print("After view")
        return response
```

Add to `MIDDLEWARE` in `settings.py`:
```python
MIDDLEWARE = [
    ...
    'app_name.middleware.SimpleMiddleware',
]
```

---

## **12. Testing**

### **Write Tests**
**tests.py**
```python
from django.test import TestCase
from .models import Book

class BookTestCase(TestCase):
    def test_book_creation(self):
        book = Book.objects.create(title="Test Book", author="Test Author")
        self.assertEqual(str(book), "Test Book")
```

### **Run Tests**
```bash
python manage.py test
```

---

## **13. Deployment**

### **Using Gunicorn**
Install and run:
```bash
pip install gunicorn
gunicorn project_name.wsgi:application
```

### **Collect Static Files**
```bash
python manage.py collectstatic
```

### **Using Heroku**
```bash
# Install Heroku CLI
heroku login

# Deploy to Heroku
git push heroku master
```

---

## **14. Key Commands Cheat Sheet**

| **Command**                        | **Description**                          |
|------------------------------------|------------------------------------------|
| `python manage.py runserver`       | Start development server                 |
| `python manage.py startapp app_name` | Create a new app                         |
| `python manage.py makemigrations`  | Create migration files                   |
| `python manage.py migrate`         | Apply migrations to the database         |
| `python manage.py createsuperuser` | Create an admin superuser                |
| `python manage.py collectstatic`   | Collect all static files for production  |
| `python manage.py test`            | Run unit tests                           |

---

This comprehensive handbook summarizes the most essential parts of Django development.
