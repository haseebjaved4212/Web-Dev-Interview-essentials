# 🎸 Django Interview Essentials

> A complete, beginner-friendly reference guide covering every Django concept you need to ace backend and full-stack developer interviews. Written in simple, easy English with clear code examples and real-world patterns.

---

## 📌 Table of Contents

- [What is Django?](#what-is-django)
- [Django vs Flask vs FastAPI](#django-vs-flask-vs-fastapi)
- [Project Structure](#project-structure)
- [Django Request Response Cycle](#django-request-response-cycle)
- [URLs and Routing](#urls-and-routing)
- [Views](#views)
- [Templates](#templates)
- [Models](#models)
- [ORM Queries](#orm-queries)
- [Migrations](#migrations)
- [Django Admin](#django-admin)
- [Forms](#forms)
- [Model Forms](#model-forms)
- [Class Based Views](#class-based-views)
- [Django REST Framework](#django-rest-framework)
- [Serializers](#serializers)
- [Authentication and Permissions](#authentication-and-permissions)
- [JWT Authentication](#jwt-authentication)
- [Middleware](#middleware)
- [Signals](#signals)
- [Celery and Task Queues](#celery-and-task-queues)
- [Caching](#caching)
- [File Uploads](#file-uploads)
- [Static and Media Files](#static-and-media-files)
- [Settings Management](#settings-management)
- [Testing in Django](#testing-in-django)
- [Security Best Practices](#security-best-practices)
- [Performance Optimization](#performance-optimization)
- [Deployment](#deployment)
- [Common Interview Questions](#common-interview-questions)

---

## What is Django?

Django is a **high-level Python web framework** that lets you build web applications fast. It was created in 2003 by Adrian Holovaty and Simon Willison, originally built to power a newspaper website. The core philosophy behind Django is "batteries included" which means it comes with almost everything you need already built in.

When you use Django you get all of this out of the box without installing extra packages:

- A URL routing system
- An ORM for talking to databases without writing raw SQL
- A templating engine for rendering HTML
- A built-in admin panel that generates itself from your models
- User authentication (login, logout, password reset)
- Form handling and validation
- Security protections (CSRF, SQL injection, XSS)
- A testing framework

Django follows two important design philosophies.

**DRY (Don't Repeat Yourself)** means every piece of logic should be written in one place and reused everywhere. If you find yourself copying and pasting code, Django probably has a better way.

**MTV (Model Template View)** is Django's version of MVC. The Model handles data, the Template handles what the user sees, and the View handles the logic in between.

```
User Request
     |
  URL Router   -- finds the right view
     |
   View        -- fetches data from models, decides what to show
     |
  Template     -- renders HTML using the data
     |
User Response
```

---

## Django vs Flask vs FastAPI

This is one of the most common comparison questions in interviews.

| Feature | Django | Flask | FastAPI |
|---|---|---|---|
| Type | Full framework | Micro framework | Modern async framework |
| Built-in ORM | Yes | No | No |
| Admin panel | Yes | No | No |
| Built-in auth | Yes | No | No |
| Learning curve | Medium | Low | Medium |
| Performance | Good | Good | Excellent (async) |
| Best for | Full web apps, CMS, APIs | Small apps, prototypes | High-performance APIs, ML serving |
| REST API support | Via DRF package | Via extensions | Built-in |

> **Interview Tip:** A strong answer sounds like this. "Django is the right choice when you need a production-ready application fast, especially when you need an admin panel, built-in auth, and a solid ORM. Flask is better for smaller, more flexible projects where you want to choose your own tools. FastAPI is better when you need very high performance async APIs, like serving machine learning models or building microservices."

---

## Project Structure

```
myproject/
|
|-- myproject/              <- Project package (same name as project)
|   |-- __init__.py
|   |-- settings.py         <- All configuration lives here
|   |-- urls.py             <- Root URL configuration
|   |-- wsgi.py             <- WSGI entry point (production)
|   |-- asgi.py             <- ASGI entry point (async/WebSockets)
|
|-- users/                  <- A Django app (feature module)
|   |-- __init__.py
|   |-- admin.py            <- Register models with admin panel
|   |-- apps.py             <- App configuration class
|   |-- models.py           <- Database models
|   |-- views.py            <- Request handling logic
|   |-- urls.py             <- App-level URL patterns
|   |-- serializers.py      <- DRF serializers (if building APIs)
|   |-- forms.py            <- Django forms
|   |-- tests.py            <- Test cases
|   |-- migrations/         <- Auto-generated database migration files
|       |-- __init__.py
|       |-- 0001_initial.py
|
|-- products/               <- Another Django app
|   |-- ...
|
|-- templates/              <- HTML templates
|   |-- base.html
|   |-- users/
|       |-- login.html
|
|-- static/                 <- CSS, JavaScript, images you write
|-- media/                  <- User-uploaded files
|-- requirements.txt        <- Python package dependencies
|-- manage.py               <- Command-line utility for Django
|-- .env                    <- Environment variables (never commit this)
```

### Project vs App

A **project** is the whole website. An **app** is one feature or module inside that project. For example a blogging website (project) might have a `users` app, a `posts` app, and a `comments` app. Each app does one thing and does it well. Apps can even be reused across different projects which is what makes Django so modular.

---

## Django Request Response Cycle

Understanding exactly what happens when a user visits a URL is always asked in interviews.

```
1. Browser sends HTTP request to your server

2. WSGI/ASGI server (Gunicorn, Uvicorn) receives it and passes to Django

3. Django runs through all MIDDLEWARE (request phase)
   - Each middleware can modify the request or stop it early
   - Common ones: SecurityMiddleware, SessionMiddleware, AuthMiddleware

4. Django looks at the URL and finds the matching pattern in urls.py

5. Django calls the matched VIEW function or class

6. The view:
   a. Reads data from MODELS (ORM queries to the database)
   b. Processes business logic
   c. Passes data to a TEMPLATE (or builds a JSON response for APIs)

7. Django runs through MIDDLEWARE again (response phase)
   - Each middleware can modify the response on the way out

8. Django sends the HTTP response back to the browser
```

---

## URLs and Routing

URL patterns tell Django which view to call for each URL.

```python
# myproject/urls.py  (root URL file)
from django.contrib import admin
from django.urls import path, include

urlpatterns = [
    path("admin/", admin.site.urls),
    path("api/users/", include("users.urls")),
    path("api/products/", include("products.urls")),
]
```

```python
# users/urls.py  (app-level URL file)
from django.urls import path
from . import views

urlpatterns = [
    path("", views.UserListView.as_view(), name="user-list"),
    path("<int:pk>/", views.UserDetailView.as_view(), name="user-detail"),
    path("register/", views.RegisterView.as_view(), name="register"),
    path("login/", views.LoginView.as_view(), name="login"),
]
```

### URL Converters

```python
# Path converters automatically convert URL segments to Python types
path("users/<int:pk>/", views.user_detail)         # pk becomes an integer
path("posts/<str:slug>/", views.post_detail)        # slug stays a string
path("files/<path:file_path>/", views.serve_file)  # path includes slashes
path("archive/<int:year>/<int:month>/", views.archive)

# re_path for complex patterns using regex
from django.urls import re_path
re_path(r"^articles/(?P<year>[0-9]{4})/$", views.year_archive)

# Naming your URL patterns lets you reference them in code and templates
path("users/<int:pk>/", views.user_detail, name="user-detail")

# Reversing URLs in Python code
from django.urls import reverse
url = reverse("user-detail", kwargs={"pk": 42})
# Result: "/api/users/42/"

# Reversing in templates
# {% url "user-detail" pk=user.pk %}
```

---

## Views

A view is a Python function or class that receives a request and returns a response.

### Function Based Views

```python
# users/views.py
from django.shortcuts import render, get_object_or_404, redirect
from django.http import JsonResponse, HttpResponse
from .models import User

def user_list(request):
    if request.method == "GET":
        users = User.objects.all()
        return render(request, "users/list.html", {"users": users})

def user_detail(request, pk):
    # get_object_or_404 is much cleaner than wrapping everything in try/except
    user = get_object_or_404(User, pk=pk)

    if request.method == "GET":
        return render(request, "users/detail.html", {"user": user})

    elif request.method == "DELETE":
        user.delete()
        return HttpResponse(status=204)

# Returning JSON directly
def user_list_json(request):
    users = list(User.objects.values("id", "name", "email"))
    return JsonResponse({"users": users})
```

### Decorators for Function Views

```python
from django.contrib.auth.decorators import login_required, permission_required
from django.views.decorators.http import require_http_methods

# Protect a view so only logged-in users can access it
@login_required(login_url="/login/")
def dashboard(request):
    return render(request, "dashboard.html")

# Only allow specific HTTP methods
@require_http_methods(["GET", "POST"])
def create_user(request):
    pass

# Require a specific permission
@permission_required("users.can_delete_users")
def delete_user(request, pk):
    pass
```

---

## Templates

Django templates are HTML files with special template tags and filters mixed in.

```html
<!-- templates/base.html -->
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8" />
    <title>{% block title %}My Site{% endblock %}</title>
    {% load static %}
    <link rel="stylesheet" href="{% static 'css/main.css' %}" />
</head>
<body>
    <nav>
        {% if user.is_authenticated %}
            <span>Hello, {{ user.username }}</span>
            <a href="{% url 'logout' %}">Logout</a>
        {% else %}
            <a href="{% url 'login' %}">Login</a>
        {% endif %}
    </nav>

    <main>
        {% block content %}
        {% endblock %}
    </main>
</body>
</html>
```

```html
<!-- templates/users/list.html -->
{% extends "base.html" %}

{% block title %}Users{% endblock %}

{% block content %}
<h1>All Users</h1>

{% if users %}
    <ul>
    {% for user in users %}
        <li>
            <a href="{% url 'user-detail' pk=user.pk %}">
                {{ user.get_full_name|default:user.username }}
            </a>
            <span>Joined: {{ user.date_joined|date:"M d, Y" }}</span>
        </li>
    {% endfor %}
    </ul>
{% else %}
    <p>No users found.</p>
{% endif %}

{% endblock %}
```

### Common Template Tags and Filters

```html
<!-- Variables -->
{{ variable }}
{{ user.first_name }}

<!-- Tags (logic) -->
{% if condition %}...{% elif other %}...{% else %}...{% endif %}
{% for item in items %}...{% empty %}...{% endfor %}
{% block name %}...{% endblock %}
{% extends "base.html" %}
{% include "partials/nav.html" %}
{% load static %}
{% url "name" arg1 arg2 %}
{% csrf_token %}
{% comment %}This is a comment{% endcomment %}

<!-- Filters -->
{{ name|lower }}
{{ name|upper }}
{{ name|title }}
{{ name|truncatewords:10 }}
{{ date|date:"Y-m-d" }}
{{ date|timesince }}
{{ list|length }}
{{ value|default:"Nothing here" }}
{{ html_content|safe }}
{{ price|floatformat:2 }}
```

---

## Models

Models are Python classes that map to database tables. This is the heart of Django.

```python
# users/models.py
from django.db import models
from django.contrib.auth.models import AbstractUser
from django.utils.translation import gettext_lazy as _


class User(AbstractUser):
    """
    Always create a custom user model at the start of a project.
    It is much harder to switch later.
    """
    email = models.EmailField(_("email address"), unique=True)
    bio = models.TextField(blank=True)
    avatar = models.ImageField(upload_to="avatars/", blank=True, null=True)
    date_of_birth = models.DateField(null=True, blank=True)

    USERNAME_FIELD = "email"
    REQUIRED_FIELDS = ["username"]

    def __str__(self):
        return self.email

    def get_full_name(self):
        return f"{self.first_name} {self.last_name}".strip()


class Category(models.Model):
    name = models.CharField(max_length=100)
    slug = models.SlugField(unique=True)
    description = models.TextField(blank=True)
    parent = models.ForeignKey(
        "self",
        on_delete=models.SET_NULL,
        null=True,
        blank=True,
        related_name="children",
    )

    class Meta:
        verbose_name_plural = "categories"
        ordering = ["name"]

    def __str__(self):
        return self.name


class Product(models.Model):

    class Status(models.TextChoices):
        DRAFT = "draft", "Draft"
        PUBLISHED = "published", "Published"
        ARCHIVED = "archived", "Archived"

    title = models.CharField(max_length=200)
    slug = models.SlugField(unique=True)
    description = models.TextField()
    price = models.DecimalField(max_digits=10, decimal_places=2)
    stock = models.PositiveIntegerField(default=0)
    status = models.CharField(
        max_length=10,
        choices=Status.choices,
        default=Status.DRAFT,
    )
    is_featured = models.BooleanField(default=False)

    # Relationships
    category = models.ForeignKey(
        Category,
        on_delete=models.PROTECT,
        related_name="products",
    )
    tags = models.ManyToManyField("Tag", blank=True, related_name="products")
    created_by = models.ForeignKey(
        User,
        on_delete=models.SET_NULL,
        null=True,
        related_name="products",
    )

    # Timestamps
    created_at = models.DateTimeField(auto_now_add=True)
    updated_at = models.DateTimeField(auto_now=True)

    class Meta:
        ordering = ["-created_at"]
        indexes = [
            models.Index(fields=["slug"]),
            models.Index(fields=["status", "created_at"]),
        ]

    def __str__(self):
        return self.title

    def is_in_stock(self):
        return self.stock > 0


class Tag(models.Model):
    name = models.CharField(max_length=50, unique=True)
    slug = models.SlugField(unique=True)

    def __str__(self):
        return self.name
```

### Field Types Reference

```python
# Text
models.CharField(max_length=200)        # short strings, requires max_length
models.TextField()                       # long text, no length limit
models.EmailField()                      # validates email format
models.URLField()                        # validates URL format
models.SlugField()                       # URL-safe strings
models.UUIDField(default=uuid.uuid4)    # UUID fields

# Numbers
models.IntegerField()
models.PositiveIntegerField()
models.BigIntegerField()
models.FloatField()
models.DecimalField(max_digits=10, decimal_places=2)  # always use for money

# Boolean
models.BooleanField(default=False)

# Date and Time
models.DateField()
models.TimeField()
models.DateTimeField()
models.DateTimeField(auto_now_add=True)   # set once on creation, never changes
models.DateTimeField(auto_now=True)       # updated on every save automatically

# Files
models.FileField(upload_to="documents/")
models.ImageField(upload_to="images/")   # requires Pillow

# Relationships
models.ForeignKey(OtherModel, on_delete=models.CASCADE)
models.ManyToManyField(OtherModel)
models.OneToOneField(OtherModel, on_delete=models.CASCADE)

# on_delete options for ForeignKey
models.CASCADE      # delete this when the related object is deleted
models.PROTECT      # prevent deleting the related object if this exists
models.SET_NULL     # set FK to null (field must have null=True)
models.SET_DEFAULT  # set FK to the default value
models.DO_NOTHING   # do nothing (dangerous, can break DB integrity)

# Common field options
null=True           # allows NULL in the database column
blank=True          # allows empty value in forms and validation
default=0           # default value when not provided
unique=True         # must be unique across the table
db_index=True       # create a database index for faster lookups
choices=MY_CHOICES  # restrict to specific values
verbose_name="Name" # human-readable name shown in admin
help_text="Enter your full name."  # shown in forms and admin
```

---

## ORM Queries

The Django ORM lets you query your database using Python instead of raw SQL. This is asked heavily in every Django interview.

```python
from users.models import User, Product, Category

# ---- CREATE ----
# create() does everything in one database call
user = User.objects.create(
    username="haseeb",
    email="haseeb@example.com",
    first_name="Haseeb",
)

# Or instantiate and save separately
user = User(username="haseeb", email="haseeb@example.com")
user.save()

# ---- READ ----
all_users    = User.objects.all()
active_users = User.objects.filter(is_active=True)
admins       = User.objects.filter(is_staff=True, is_active=True)
non_admins   = User.objects.exclude(is_staff=True)

# Get a single record (raises exception if not found or if multiple found)
user = User.objects.get(pk=1)
user = User.objects.get(email="haseeb@example.com")

# Safe single record with automatic 404
from django.shortcuts import get_object_or_404
user = get_object_or_404(User, pk=pk)

# Checking records
first_user = User.objects.first()
last_user  = User.objects.last()
has_users  = User.objects.exists()
user_count = User.objects.count()

# ---- FIELD LOOKUPS ----
# Double underscore (__) is Django's filter lookup separator
User.objects.filter(username__exact="haseeb")
User.objects.filter(username__iexact="Haseeb")      # case-insensitive
User.objects.filter(username__contains="hase")
User.objects.filter(username__icontains="Hase")     # case-insensitive contains
User.objects.filter(username__startswith="ha")
User.objects.filter(username__endswith="eb")
User.objects.filter(date_joined__year=2024)
User.objects.filter(date_joined__month=6)
User.objects.filter(age__gt=18)      # greater than
User.objects.filter(age__gte=18)     # greater than or equal
User.objects.filter(age__lt=65)      # less than
User.objects.filter(age__lte=65)     # less than or equal
User.objects.filter(id__in=[1, 2, 3])
User.objects.filter(bio__isnull=True)
User.objects.filter(bio__isnull=False)

# ---- UPDATE ----
user = User.objects.get(pk=1)
user.first_name = "New Name"
user.save()

# Save only specific fields (much more efficient)
user.save(update_fields=["first_name"])

# Bulk update with one SQL statement
User.objects.filter(is_active=False).update(is_active=True)
User.objects.filter(pk__in=[1, 2, 3]).update(status="archived")

# ---- DELETE ----
user = User.objects.get(pk=1)
user.delete()

User.objects.filter(is_active=False).delete()

# ---- ORDERING ----
User.objects.order_by("username")
User.objects.order_by("-date_joined")             # descending (notice the minus sign)
User.objects.order_by("last_name", "first_name")  # multiple fields

# ---- SLICING (Limiting results) ----
first_ten = User.objects.all()[:10]
next_ten  = User.objects.all()[10:20]

# ---- VALUES AND VALUES LIST ----
# Return dictionaries instead of model instances (faster, uses less memory)
User.objects.values("id", "username", "email")
# Result: [{"id": 1, "username": "haseeb", "email": "..."}, ...]

# Return tuples
User.objects.values_list("id", "username")
# Result: [(1, "haseeb"), (2, "ahmed"), ...]

# Return a flat list of one field
User.objects.values_list("username", flat=True)
# Result: ["haseeb", "ahmed", "sara"]

# ---- RELATED OBJECTS ----
# select_related: for ForeignKey and OneToOne (does a SQL JOIN, one query)
products = Product.objects.select_related("category", "created_by").all()

# prefetch_related: for ManyToMany and reverse ForeignKey (separate query, Python join)
products = Product.objects.prefetch_related("tags").all()

# Combine both
products = Product.objects.select_related("category").prefetch_related("tags")

# Filter across relationships using double underscore
Product.objects.filter(category__name="Electronics")
Product.objects.filter(category__parent__name="Tech")
User.objects.filter(products__status="published").distinct()

# ---- AGGREGATION ----
from django.db.models import Count, Sum, Avg, Max, Min

Product.objects.aggregate(
    total=Count("id"),
    avg_price=Avg("price"),
    total_value=Sum("price"),
    max_price=Max("price"),
)

# annotate: add a computed field to each object in the queryset
Category.objects.annotate(product_count=Count("products"))
User.objects.annotate(num_products=Count("products")).order_by("-num_products")

# ---- Q OBJECTS (complex OR / AND / NOT conditions) ----
from django.db.models import Q

# OR condition
Product.objects.filter(Q(status="published") | Q(is_featured=True))

# AND with OR
Product.objects.filter(
    Q(status="published") & (Q(price__lt=100) | Q(is_featured=True))
)

# NOT condition
Product.objects.filter(~Q(status="archived"))

# ---- F OBJECTS (reference another field in a query) ----
from django.db.models import F

# Find products where price is greater than original_price
Product.objects.filter(price__gt=F("original_price"))

# Increment stock without loading the object into Python
Product.objects.filter(pk=1).update(stock=F("stock") - 1)

# ---- get_or_create and update_or_create ----
user, created = User.objects.get_or_create(
    email="haseeb@example.com",
    defaults={"username": "haseeb", "first_name": "Haseeb"},
)

product, created = Product.objects.update_or_create(
    slug="my-product",
    defaults={"title": "Updated Title", "price": 99.99},
)

# ---- QUERYSET LAZINESS ----
# Querysets are lazy -- nothing hits the database until you actually evaluate them
qs = User.objects.all()
qs = qs.filter(is_active=True)
qs = qs.exclude(is_staff=True)
qs = qs.order_by("username")
# Still no database query at this point!

users = list(qs)   # NOW it hits the database with a single optimized query
```

---

## Migrations

Migrations are Django's way of tracking changes to your models and applying them to the actual database schema.

```bash
# Create migration files from model changes
python manage.py makemigrations

# Create for a specific app only
python manage.py makemigrations users

# Apply all pending migrations
python manage.py migrate

# Apply for a specific app
python manage.py migrate users

# See which migrations are applied and which are pending
python manage.py showmigrations

# Roll back to a specific migration
python manage.py migrate users 0003

# Roll back ALL migrations for an app
python manage.py migrate users zero

# Squash many migrations into one (useful after a project matures)
python manage.py squashmigrations users 0001 0010

# Create an empty migration for custom SQL or data migrations
python manage.py makemigrations --empty users
```

### Data Migration Example

```python
# users/migrations/0002_populate_slugs.py
from django.db import migrations
from django.utils.text import slugify

def populate_slugs(apps, schema_editor):
    # Always use apps.get_model inside migrations, NOT a direct model import
    # This gives you the historical version of the model at this exact point in time
    Product = apps.get_model("products", "Product")

    for product in Product.objects.all():
        product.slug = slugify(product.title)
        product.save(update_fields=["slug"])

def reverse_populate_slugs(apps, schema_editor):
    Product = apps.get_model("products", "Product")
    Product.objects.all().update(slug="")

class Migration(migrations.Migration):
    dependencies = [
        ("products", "0001_initial"),
    ]

    operations = [
        migrations.RunPython(populate_slugs, reverse_populate_slugs),
    ]
```

> **Interview Tip:** A very common question is "What do you do if two developers create migrations at the same time on different branches?" Django will detect the conflict when you try to merge. The fix is to run `python manage.py makemigrations --merge` which creates a merge migration that resolves the conflict by making one depend on the other.

---

## Django Admin

The Django admin panel is automatically generated from your models. It is one of the biggest advantages Django has over other frameworks.

```python
# users/admin.py
from django.contrib import admin
from django.contrib.auth.admin import UserAdmin as BaseUserAdmin
from .models import User, Product, Category


@admin.register(User)
class UserAdmin(BaseUserAdmin):
    list_display  = ["email", "username", "first_name", "is_active", "date_joined"]
    list_filter   = ["is_active", "is_staff", "date_joined"]
    search_fields = ["email", "username", "first_name", "last_name"]
    ordering      = ["-date_joined"]
    readonly_fields = ["date_joined", "last_login"]

    fieldsets = BaseUserAdmin.fieldsets + (
        ("Profile", {"fields": ("bio", "avatar", "date_of_birth")}),
    )


@admin.register(Category)
class CategoryAdmin(admin.ModelAdmin):
    list_display       = ["name", "slug", "parent"]
    search_fields      = ["name"]
    prepopulated_fields = {"slug": ("name",)}   # auto-fills slug from name


@admin.register(Product)
class ProductAdmin(admin.ModelAdmin):
    list_display    = ["title", "category", "price", "stock", "status", "created_at"]
    list_filter     = ["status", "category", "is_featured"]
    search_fields   = ["title", "description"]
    list_editable   = ["price", "status"]        # edit directly in the list view
    prepopulated_fields = {"slug": ("title",)}
    readonly_fields = ["created_at", "updated_at"]
    filter_horizontal = ["tags"]                 # nicer widget for ManyToMany

    fieldsets = [
        ("Basic Info", {
            "fields": ("title", "slug", "description", "category"),
        }),
        ("Pricing and Stock", {
            "fields": ("price", "stock"),
        }),
        ("Settings", {
            "fields": ("status", "is_featured", "tags", "created_by"),
            "classes": ("collapse",),
        }),
        ("Timestamps", {
            "fields": ("created_at", "updated_at"),
        }),
    ]

    actions = ["make_published"]

    @admin.action(description="Mark selected products as published")
    def make_published(self, request, queryset):
        updated = queryset.update(status="published")
        self.message_user(request, f"{updated} products published successfully.")
```

---

## Forms

Django forms handle input validation and HTML form rendering for you automatically.

```python
# users/forms.py
from django import forms
from django.contrib.auth import get_user_model
from django.contrib.auth.password_validation import validate_password

User = get_user_model()

class RegisterForm(forms.Form):
    first_name = forms.CharField(
        max_length=50,
        widget=forms.TextInput(attrs={"placeholder": "First name", "class": "form-input"}),
    )
    last_name = forms.CharField(max_length=50)
    email     = forms.EmailField()
    password  = forms.CharField(
        widget=forms.PasswordInput(),
        validators=[validate_password],
    )
    confirm_password = forms.CharField(widget=forms.PasswordInput())
    agree_to_terms   = forms.BooleanField(required=True)

    def clean_email(self):
        """Field-level validation. Method name must be clean_ + field_name."""
        email = self.cleaned_data["email"].lower()
        if User.objects.filter(email=email).exists():
            raise forms.ValidationError("An account with this email already exists.")
        return email

    def clean(self):
        """Cross-field validation. Runs after all individual field validations."""
        cleaned_data = super().clean()
        password         = cleaned_data.get("password")
        confirm_password = cleaned_data.get("confirm_password")

        if password and confirm_password and password != confirm_password:
            raise forms.ValidationError("Passwords do not match.")

        return cleaned_data
```

```python
# Using the form in a view
def register(request):
    if request.method == "POST":
        form = RegisterForm(request.POST)
        if form.is_valid():
            email    = form.cleaned_data["email"]
            password = form.cleaned_data["password"]
            User.objects.create_user(email=email, password=password)
            return redirect("login")
    else:
        form = RegisterForm()

    return render(request, "users/register.html", {"form": form})
```

```html
<!-- In the template -->
<form method="post">
    {% csrf_token %}
    {{ form.as_p }}
    <button type="submit">Register</button>
</form>

<!-- Render each field manually for custom styling -->
{% for field in form %}
    <div class="field">
        {{ field.label_tag }}
        {{ field }}
        {% if field.errors %}
            <ul class="errors">
                {% for error in field.errors %}
                    <li>{{ error }}</li>
                {% endfor %}
            </ul>
        {% endif %}
    </div>
{% endfor %}
```

---

## Model Forms

Model Forms are generated automatically from a model. This saves you from writing the same fields in both your model and your form.

```python
# products/forms.py
from django import forms
from .models import Product

class ProductForm(forms.ModelForm):
    class Meta:
        model  = Product
        fields = ["title", "description", "price", "stock", "category", "tags", "status"]

        widgets = {
            "description": forms.Textarea(attrs={"rows": 4}),
            "price":       forms.NumberInput(attrs={"step": "0.01"}),
        }

        labels = {
            "is_featured": "Feature this product on the homepage",
        }

    def clean_price(self):
        price = self.cleaned_data["price"]
        if price <= 0:
            raise forms.ValidationError("Price must be greater than zero.")
        return price

    def save(self, commit=True):
        product = super().save(commit=False)   # get the instance without hitting the DB
        product.slug = slugify(product.title)  # add custom logic before saving
        if commit:
            product.save()
            self.save_m2m()  # ManyToMany must be saved manually when commit=False
        return product
```

```python
# Create view
def create_product(request):
    if request.method == "POST":
        form = ProductForm(request.POST)
        if form.is_valid():
            product = form.save(commit=False)
            product.created_by = request.user
            product.save()
            form.save_m2m()
            return redirect("product-detail", pk=product.pk)
    else:
        form = ProductForm()

    return render(request, "products/create.html", {"form": form})

# Edit view -- just pass the instance to pre-fill the form
def edit_product(request, pk):
    product = get_object_or_404(Product, pk=pk)

    if request.method == "POST":
        form = ProductForm(request.POST, instance=product)
        if form.is_valid():
            form.save()
            return redirect("product-detail", pk=product.pk)
    else:
        form = ProductForm(instance=product)

    return render(request, "products/edit.html", {"form": form, "product": product})
```

---

## Class Based Views

Class Based Views reduce repetition for common patterns by using Django's built-in generic views.

```python
from django.views import View
from django.views.generic import (
    ListView, DetailView, CreateView, UpdateView, DeleteView
)
from django.contrib.auth.mixins import LoginRequiredMixin, PermissionRequiredMixin
from django.urls import reverse_lazy
from .models import Product
from .forms import ProductForm


class ProductListView(ListView):
    model               = Product
    template_name       = "products/list.html"
    context_object_name = "products"
    paginate_by         = 12

    def get_queryset(self):
        qs     = super().get_queryset()
        status = self.request.GET.get("status")
        if status:
            qs = qs.filter(status=status)
        return qs.select_related("category")

    def get_context_data(self, **kwargs):
        context = super().get_context_data(**kwargs)
        context["categories"] = Category.objects.all()
        return context


class ProductDetailView(DetailView):
    model               = Product
    template_name       = "products/detail.html"
    context_object_name = "product"


class ProductCreateView(LoginRequiredMixin, CreateView):
    model         = Product
    form_class    = ProductForm
    template_name = "products/form.html"
    success_url   = reverse_lazy("product-list")

    def form_valid(self, form):
        form.instance.created_by = self.request.user
        return super().form_valid(form)


class ProductUpdateView(LoginRequiredMixin, UpdateView):
    model         = Product
    form_class    = ProductForm
    template_name = "products/form.html"

    def get_success_url(self):
        return reverse_lazy("product-detail", kwargs={"pk": self.object.pk})


class ProductDeleteView(LoginRequiredMixin, PermissionRequiredMixin, DeleteView):
    model                = Product
    template_name        = "products/confirm_delete.html"
    success_url          = reverse_lazy("product-list")
    permission_required  = "products.delete_product"


# Custom view using the base View class
class ProductToggleFeaturedView(LoginRequiredMixin, View):
    def post(self, request, pk):
        product = get_object_or_404(Product, pk=pk)
        product.is_featured = not product.is_featured
        product.save(update_fields=["is_featured"])
        return redirect("product-detail", pk=pk)
```

---

## Django REST Framework

Django REST Framework (DRF) is the standard package for building REST APIs with Django.

```bash
pip install djangorestframework django-filter
```

```python
# settings.py
INSTALLED_APPS = [
    ...
    "rest_framework",
    "django_filters",
]

REST_FRAMEWORK = {
    "DEFAULT_AUTHENTICATION_CLASSES": [
        "rest_framework_simplejwt.authentication.JWTAuthentication",
    ],
    "DEFAULT_PERMISSION_CLASSES": [
        "rest_framework.permissions.IsAuthenticated",
    ],
    "DEFAULT_PAGINATION_CLASS": "rest_framework.pagination.PageNumberPagination",
    "PAGE_SIZE": 10,
    "DEFAULT_THROTTLE_CLASSES": [
        "rest_framework.throttling.AnonRateThrottle",
        "rest_framework.throttling.UserRateThrottle",
    ],
    "DEFAULT_THROTTLE_RATES": {
        "anon": "100/day",
        "user": "1000/day",
    },
}
```

### ViewSets and Routers

```python
# products/views.py
from rest_framework import viewsets, filters
from rest_framework.decorators import action
from rest_framework.response import Response
from rest_framework.permissions import IsAuthenticated, AllowAny
from django_filters.rest_framework import DjangoFilterBackend
from .models import Product
from .serializers import ProductSerializer, ProductDetailSerializer


class ProductViewSet(viewsets.ModelViewSet):
    """
    A ViewSet automatically provides list, create, retrieve,
    update, and destroy actions.
    """
    queryset         = Product.objects.select_related("category", "created_by").prefetch_related("tags")
    serializer_class = ProductSerializer

    filter_backends  = [DjangoFilterBackend, filters.SearchFilter, filters.OrderingFilter]
    filterset_fields = ["status", "category", "is_featured"]
    search_fields    = ["title", "description"]
    ordering_fields  = ["price", "created_at", "title"]
    ordering         = ["-created_at"]

    def get_serializer_class(self):
        if self.action in ["retrieve", "create", "update", "partial_update"]:
            return ProductDetailSerializer
        return ProductSerializer

    def get_permissions(self):
        if self.action in ["list", "retrieve"]:
            return [AllowAny()]
        return [IsAuthenticated()]

    def perform_create(self, serializer):
        serializer.save(created_by=self.request.user)

    def get_queryset(self):
        qs = super().get_queryset()
        if not self.request.user.is_staff:
            qs = qs.filter(status="published")
        return qs

    # Custom action: POST /api/products/{pk}/toggle-featured/
    @action(detail=True, methods=["post"], permission_classes=[IsAuthenticated])
    def toggle_featured(self, request, pk=None):
        product             = self.get_object()
        product.is_featured = not product.is_featured
        product.save(update_fields=["is_featured"])
        return Response({"is_featured": product.is_featured})

    # Custom list action: GET /api/products/featured/
    @action(detail=False, methods=["get"])
    def featured(self, request):
        featured   = self.get_queryset().filter(is_featured=True)
        serializer = self.get_serializer(featured, many=True)
        return Response(serializer.data)
```

```python
# products/urls.py
from django.urls import path, include
from rest_framework.routers import DefaultRouter
from . import views

router = DefaultRouter()
router.register("products", views.ProductViewSet, basename="product")

urlpatterns = [
    path("", include(router.urls)),
]

# The router automatically creates these URLs:
# GET    /products/          -> list
# POST   /products/          -> create
# GET    /products/{pk}/     -> retrieve
# PUT    /products/{pk}/     -> update
# PATCH  /products/{pk}/     -> partial_update
# DELETE /products/{pk}/     -> destroy
# POST   /products/{pk}/toggle-featured/
# GET    /products/featured/
```

---

## Serializers

Serializers convert model instances to JSON (for API responses) and validate incoming JSON (for API requests).

```python
# products/serializers.py
from rest_framework import serializers
from django.contrib.auth import get_user_model
from .models import Product, Category, Tag

User = get_user_model()


class TagSerializer(serializers.ModelSerializer):
    class Meta:
        model  = Tag
        fields = ["id", "name", "slug"]


class CategorySerializer(serializers.ModelSerializer):
    class Meta:
        model  = Category
        fields = ["id", "name", "slug"]


class AuthorSerializer(serializers.ModelSerializer):
    class Meta:
        model  = User
        fields = ["id", "username", "email"]


# Lightweight serializer for list views
class ProductSerializer(serializers.ModelSerializer):
    category_name = serializers.CharField(source="category.name", read_only=True)
    tags          = TagSerializer(many=True, read_only=True)

    class Meta:
        model  = Product
        fields = ["id", "title", "slug", "price", "status", "category_name", "tags", "created_at"]


# Full serializer for single item views
class ProductDetailSerializer(serializers.ModelSerializer):
    category = CategorySerializer(read_only=True)
    category_id = serializers.PrimaryKeyRelatedField(
        queryset=Category.objects.all(),
        write_only=True,
        source="category",
    )
    tags = TagSerializer(many=True, read_only=True)
    tag_ids = serializers.PrimaryKeyRelatedField(
        queryset=Tag.objects.all(),
        many=True,
        write_only=True,
        source="tags",
    )
    created_by  = AuthorSerializer(read_only=True)
    is_in_stock = serializers.SerializerMethodField()

    class Meta:
        model  = Product
        fields = [
            "id", "title", "slug", "description", "price", "stock",
            "status", "is_featured", "category", "category_id",
            "tags", "tag_ids", "created_by", "is_in_stock",
            "created_at", "updated_at",
        ]
        read_only_fields = ["slug", "created_by", "created_at", "updated_at"]

    def get_is_in_stock(self, obj):
        return obj.stock > 0

    def validate_price(self, value):
        """Field-level validation."""
        if value <= 0:
            raise serializers.ValidationError("Price must be greater than zero.")
        return value

    def validate(self, attrs):
        """Object-level validation for cross-field checks."""
        if attrs.get("status") == "published" and attrs.get("stock", 0) == 0:
            raise serializers.ValidationError(
                "Cannot publish a product with zero stock."
            )
        return attrs

    def create(self, validated_data):
        tags    = validated_data.pop("tags", [])
        product = Product.objects.create(**validated_data)
        product.tags.set(tags)
        return product

    def update(self, instance, validated_data):
        tags     = validated_data.pop("tags", None)
        instance = super().update(instance, validated_data)
        if tags is not None:
            instance.tags.set(tags)
        return instance
```

---

## Authentication and Permissions

```python
# Custom permission class
from rest_framework.permissions import BasePermission, SAFE_METHODS

class IsOwnerOrReadOnly(BasePermission):
    """Allow read access to everyone, write access only to the owner."""

    def has_object_permission(self, request, view, obj):
        if request.method in SAFE_METHODS:
            return True
        return obj.created_by == request.user


class IsAdminOrReadOnly(BasePermission):
    """Read-only for everyone, full access for admin users."""

    def has_permission(self, request, view):
        if request.method in SAFE_METHODS:
            return True
        return request.user.is_authenticated and request.user.is_staff


# Using permissions on a ViewSet
class ProductViewSet(viewsets.ModelViewSet):
    permission_classes = [IsOwnerOrReadOnly]
```

```python
# Built-in DRF permissions
from rest_framework.permissions import (
    AllowAny,                     # no restrictions at all
    IsAuthenticated,              # must be logged in
    IsAdminUser,                  # must be an admin
    IsAuthenticatedOrReadOnly,    # GET allowed for everyone, others require login
)
```

---

## JWT Authentication

```bash
pip install djangorestframework-simplejwt
```

```python
# settings.py
from datetime import timedelta

SIMPLE_JWT = {
    "ACCESS_TOKEN_LIFETIME":  timedelta(minutes=15),
    "REFRESH_TOKEN_LIFETIME": timedelta(days=7),
    "ROTATE_REFRESH_TOKENS":  True,
    "BLACKLIST_AFTER_ROTATION": True,
    "AUTH_HEADER_TYPES": ("Bearer",),
}
```

```python
# urls.py
from rest_framework_simplejwt.views import (
    TokenObtainPairView,
    TokenRefreshView,
    TokenVerifyView,
)

urlpatterns = [
    path("api/auth/login/",   TokenObtainPairView.as_view(),  name="token_obtain_pair"),
    path("api/auth/refresh/", TokenRefreshView.as_view(),     name="token_refresh"),
    path("api/auth/verify/",  TokenVerifyView.as_view(),      name="token_verify"),
]
```

```python
# Customize the JWT payload to include extra user info
from rest_framework_simplejwt.serializers import TokenObtainPairSerializer
from rest_framework_simplejwt.views import TokenObtainPairView

class CustomTokenObtainPairSerializer(TokenObtainPairSerializer):
    @classmethod
    def get_token(cls, user):
        token = super().get_token(user)
        token["email"]    = user.email
        token["name"]     = user.get_full_name()
        token["is_admin"] = user.is_staff
        return token

class CustomTokenObtainPairView(TokenObtainPairView):
    serializer_class = CustomTokenObtainPairSerializer
```

---

## Middleware

Middleware is code that runs for every single request and response, forming a pipeline around your views.

```python
# common/middleware.py
import time
import logging

logger = logging.getLogger(__name__)

class RequestLoggingMiddleware:
    """Logs every request along with how long it took to process."""

    def __init__(self, get_response):
        self.get_response = get_response

    def __call__(self, request):
        start_time = time.time()

        response = self.get_response(request)

        duration = time.time() - start_time
        logger.info(
            f"{request.method} {request.path} "
            f"[{response.status_code}] {duration:.3f}s"
        )
        return response

    def process_exception(self, request, exception):
        """Called if the view raises an exception."""
        logger.error(f"Exception on {request.path}: {exception}")
        return None


class MaintenanceModeMiddleware:
    """Block all requests when maintenance mode is active."""

    def __init__(self, get_response):
        self.get_response = get_response

    def __call__(self, request):
        from django.conf import settings
        from django.http import HttpResponse

        if getattr(settings, "MAINTENANCE_MODE", False):
            if not request.path.startswith("/admin"):
                return HttpResponse("Down for maintenance. Be right back!", status=503)

        return self.get_response(request)
```

```python
# settings.py
MIDDLEWARE = [
    "django.middleware.security.SecurityMiddleware",
    "django.contrib.sessions.middleware.SessionMiddleware",
    "django.middleware.common.CommonMiddleware",
    "django.middleware.csrf.CsrfViewMiddleware",
    "django.contrib.auth.middleware.AuthenticationMiddleware",
    "django.contrib.messages.middleware.MessageMiddleware",
    "django.middleware.clickjacking.XFrameOptionsMiddleware",
    "common.middleware.RequestLoggingMiddleware",     # your custom middleware
]
```

---

## Signals

Signals let different parts of your app communicate when events happen, without them being directly coupled together.

```python
# users/signals.py
from django.db.models.signals import post_save
from django.contrib.auth.signals import user_logged_in, user_login_failed
from django.dispatch import receiver
from django.contrib.auth import get_user_model
from .models import Profile

User = get_user_model()


@receiver(post_save, sender=User)
def create_user_profile(sender, instance, created, **kwargs):
    """Automatically create a Profile when a new User is created."""
    if created:
        Profile.objects.create(user=instance)


@receiver(post_save, sender=User)
def save_user_profile(sender, instance, **kwargs):
    """Keep the Profile in sync whenever the User is saved."""
    if hasattr(instance, "profile"):
        instance.profile.save()


@receiver(user_logged_in)
def on_user_login(sender, request, user, **kwargs):
    """Track login activity for auditing."""
    print(f"User {user.email} logged in from {request.META.get('REMOTE_ADDR')}")


@receiver(user_login_failed)
def on_login_failed(sender, credentials, request, **kwargs):
    """Log failed login attempts for security monitoring."""
    print(f"Failed login for {credentials.get('email')}")
```

```python
# users/apps.py -- connect signals when the app starts
from django.apps import AppConfig

class UsersConfig(AppConfig):
    default_auto_field = "django.db.models.BigAutoField"
    name               = "users"

    def ready(self):
        import users.signals   # this connects all the signal handlers
```

> **Interview Tip:** Signals are useful for cross-cutting concerns like sending a welcome email when a user registers or auto-creating related records. But they can make code hard to follow because the connection is implicit. For logic that is directly tied to the model, overriding the `save()` method is often more explicit and easier to test. Use signals when you want to keep things truly decoupled.

---

## Celery and Task Queues

Celery lets you run slow or heavy tasks in the background so your API response stays fast.

```bash
pip install celery redis
```

```python
# myproject/celery.py
import os
from celery import Celery

os.environ.setdefault("DJANGO_SETTINGS_MODULE", "myproject.settings")

app = Celery("myproject")
app.config_from_object("django.conf:settings", namespace="CELERY")
app.autodiscover_tasks()
```

```python
# myproject/__init__.py
from .celery import app as celery_app
__all__ = ("celery_app",)
```

```python
# settings.py
CELERY_BROKER_URL    = "redis://localhost:6379/0"
CELERY_RESULT_BACKEND = "redis://localhost:6379/0"
CELERY_ACCEPT_CONTENT = ["json"]
CELERY_TASK_SERIALIZER = "json"
```

```python
# users/tasks.py
from celery import shared_task
from django.core.mail import send_mail
from django.conf import settings


@shared_task(bind=True, max_retries=3)
def send_welcome_email(self, user_id):
    """Send a welcome email. Retries up to 3 times on failure."""
    try:
        from django.contrib.auth import get_user_model
        User = get_user_model()
        user = User.objects.get(pk=user_id)
        send_mail(
            subject="Welcome to our platform!",
            message=f"Hi {user.first_name}, welcome aboard!",
            from_email=settings.DEFAULT_FROM_EMAIL,
            recipient_list=[user.email],
        )
    except Exception as exc:
        raise self.retry(exc=exc, countdown=60)


@shared_task
def generate_monthly_report():
    """Periodic task that runs on a schedule."""
    pass
```

```python
# Calling tasks from a view
from users.tasks import send_welcome_email

def register(request):
    # ... create user ...
    send_welcome_email.delay(user.id)     # fire and forget, returns immediately
    return redirect("home")
```

```bash
# Run the Celery worker
celery -A myproject worker --loglevel=info

# Run the Celery beat scheduler for periodic tasks
celery -A myproject beat --loglevel=info
```

---

## Caching

Caching stores the results of expensive operations so you do not repeat them on every request.

```python
# settings.py
CACHES = {
    "default": {
        "BACKEND": "django.core.cache.backends.redis.RedisCache",
        "LOCATION": "redis://127.0.0.1:6379/1",
    }
}
```

```python
from django.core.cache import cache
from django.views.decorators.cache import cache_page
from django.utils.decorators import method_decorator

# Cache an entire view for 15 minutes
@cache_page(60 * 15)
def product_list(request):
    products = Product.objects.all()
    return render(request, "products/list.html", {"products": products})

# Cache a Class Based View
class ProductListView(ListView):
    @method_decorator(cache_page(60 * 15))
    def dispatch(self, *args, **kwargs):
        return super().dispatch(*args, **kwargs)

# Manual caching
def get_featured_products():
    cache_key = "featured_products"
    products  = cache.get(cache_key)

    if products is None:
        products = list(
            Product.objects.filter(is_featured=True)
            .select_related("category")[:12]
        )
        cache.set(cache_key, products, timeout=60 * 30)

    return products

# Always invalidate the cache when data changes
def update_product(request, pk):
    product = get_object_or_404(Product, pk=pk)
    # ... update product ...
    cache.delete("featured_products")
    cache.delete(f"product_{pk}")
    return redirect("product-detail", pk=pk)

# Low-level cache API
cache.set("my_key", "my_value", timeout=300)
value = cache.get("my_key", default="fallback")
cache.delete("my_key")
cache.clear()
result = cache.get_or_set("total_value", expensive_computation, timeout=600)
```

---

## File Uploads

```python
# models.py
import uuid
import os

def user_avatar_upload_path(instance, filename):
    """Generate a unique, safe filename for every upload."""
    ext      = filename.split(".")[-1]
    filename = f"{uuid.uuid4()}.{ext}"
    return os.path.join("avatars", str(instance.id), filename)

class UserProfile(models.Model):
    user     = models.OneToOneField(User, on_delete=models.CASCADE)
    avatar   = models.ImageField(upload_to=user_avatar_upload_path, blank=True, null=True)
    document = models.FileField(upload_to="documents/", blank=True)
```

```python
# DRF view for handling file uploads
from rest_framework.parsers import MultiPartParser, FormParser
from rest_framework.views import APIView

class AvatarUploadView(APIView):
    parser_classes    = [MultiPartParser, FormParser]
    permission_classes = [IsAuthenticated]

    def post(self, request):
        serializer = AvatarUploadSerializer(
            request.user.profile,
            data=request.data,
            partial=True,
        )
        serializer.is_valid(raise_exception=True)
        serializer.save()
        return Response(serializer.data)
```

```python
# Validating uploaded files in a serializer
class AvatarUploadSerializer(serializers.ModelSerializer):
    class Meta:
        model  = UserProfile
        fields = ["avatar"]

    def validate_avatar(self, value):
        max_size     = 5 * 1024 * 1024   # 5MB
        allowed_types = ["image/jpeg", "image/png", "image/webp"]

        if value.size > max_size:
            raise serializers.ValidationError("Image must be smaller than 5MB.")

        if value.content_type not in allowed_types:
            raise serializers.ValidationError("Only JPEG, PNG, and WebP images are allowed.")

        return value
```

---

## Static and Media Files

```python
# settings.py

# Static files (CSS, JavaScript, images you write yourself)
STATIC_URL   = "/static/"
STATICFILES_DIRS = [BASE_DIR / "static"]   # your static files live here
STATIC_ROOT  = BASE_DIR / "staticfiles"    # where collectstatic puts them

# Media files (files uploaded by users)
MEDIA_URL  = "/media/"
MEDIA_ROOT = BASE_DIR / "media"
```

```python
# myproject/urls.py -- serve media files during development only
from django.conf import settings
from django.conf.urls.static import static

urlpatterns = [
    ...
] + static(settings.MEDIA_URL, document_root=settings.MEDIA_ROOT)
# In production, serve media files through nginx or a CDN, not Django itself
```

```bash
# Collect all static files into STATIC_ROOT for production
python manage.py collectstatic
```

---

## Settings Management

```python
# settings/base.py -- shared settings for all environments
from pathlib import Path
from decouple import config   # pip install python-decouple

BASE_DIR   = Path(__file__).resolve().parent.parent.parent
SECRET_KEY = config("SECRET_KEY")
DEBUG      = config("DEBUG", default=False, cast=bool)
ALLOWED_HOSTS = config("ALLOWED_HOSTS", default="localhost").split(",")

INSTALLED_APPS = [
    "django.contrib.admin",
    "django.contrib.auth",
    "django.contrib.contenttypes",
    "django.contrib.sessions",
    "django.contrib.messages",
    "django.contrib.staticfiles",
    "rest_framework",
    "corsheaders",
    "django_filters",
    # local apps
    "users",
    "products",
]

AUTH_USER_MODEL = "users.User"
LANGUAGE_CODE   = "en-us"
TIME_ZONE       = "UTC"
USE_TZ          = True
```

```python
# settings/development.py
from .base import *

DEBUG = True
DATABASES = {
    "default": {
        "ENGINE": "django.db.backends.sqlite3",
        "NAME": BASE_DIR / "db.sqlite3",
    }
}
EMAIL_BACKEND = "django.core.mail.backends.console.EmailBackend"
```

```python
# settings/production.py
from .base import *
import dj_database_url

DEBUG     = False
DATABASES = {"default": dj_database_url.config(conn_max_age=600)}

# HTTPS security settings
SECURE_SSL_REDIRECT               = True
SECURE_HSTS_SECONDS               = 31536000
SECURE_HSTS_INCLUDE_SUBDOMAINS    = True
SESSION_COOKIE_SECURE             = True
CSRF_COOKIE_SECURE                = True
X_FRAME_OPTIONS                   = "DENY"

EMAIL_BACKEND      = "django.core.mail.backends.smtp.EmailBackend"
EMAIL_HOST         = config("EMAIL_HOST")
EMAIL_PORT         = config("EMAIL_PORT", cast=int)
EMAIL_HOST_USER    = config("EMAIL_HOST_USER")
EMAIL_HOST_PASSWORD = config("EMAIL_HOST_PASSWORD")
EMAIL_USE_TLS      = True
```

```ini
# .env file (never commit this to version control)
SECRET_KEY=your-super-secret-key-here
DEBUG=True
DATABASE_URL=postgresql://user:password@localhost:5432/mydb
ALLOWED_HOSTS=localhost,127.0.0.1
```

---

## Testing in Django

```python
# users/tests.py
from django.test import TestCase
from rest_framework.test import APITestCase, APIClient
from rest_framework import status
from django.contrib.auth import get_user_model
from django.urls import reverse
from .models import Product, Category

User = get_user_model()


class ProductModelTest(TestCase):
    def setUp(self):
        self.category = Category.objects.create(name="Electronics", slug="electronics")
        self.product  = Product.objects.create(
            title="Laptop",
            slug="laptop",
            description="A great laptop",
            price=999.99,
            stock=10,
            status="published",
            category=self.category,
        )

    def test_product_str(self):
        self.assertEqual(str(self.product), "Laptop")

    def test_is_in_stock(self):
        self.assertTrue(self.product.is_in_stock())

    def test_out_of_stock(self):
        self.product.stock = 0
        self.product.save()
        self.assertFalse(self.product.is_in_stock())


class ProductAPITest(APITestCase):
    def setUp(self):
        self.client   = APIClient()
        self.user     = User.objects.create_user(
            username="testuser",
            email="test@example.com",
            password="testpass123",
        )
        self.category = Category.objects.create(name="Electronics", slug="electronics")
        self.product  = Product.objects.create(
            title="Laptop",
            slug="laptop",
            description="A great laptop",
            price=999.99,
            stock=10,
            status="published",
            category=self.category,
            created_by=self.user,
        )

    def test_list_products_unauthenticated(self):
        url      = reverse("product-list")
        response = self.client.get(url)
        self.assertEqual(response.status_code, status.HTTP_200_OK)

    def test_create_product_unauthenticated(self):
        url      = reverse("product-list")
        response = self.client.post(url, {"title": "Phone"})
        self.assertEqual(response.status_code, status.HTTP_401_UNAUTHORIZED)

    def test_create_product_authenticated(self):
        self.client.force_authenticate(user=self.user)
        url  = reverse("product-list")
        data = {
            "title":       "Phone",
            "slug":        "phone",
            "description": "A smartphone",
            "price":       "499.99",
            "stock":       5,
            "category_id": self.category.pk,
        }
        response = self.client.post(url, data, format="json")
        self.assertEqual(response.status_code, status.HTTP_201_CREATED)
        self.assertEqual(Product.objects.count(), 2)

    def test_update_product_not_owner(self):
        other_user = User.objects.create_user(
            username="other", email="other@test.com", password="pass"
        )
        self.client.force_authenticate(user=other_user)
        url      = reverse("product-detail", kwargs={"pk": self.product.pk})
        response = self.client.patch(url, {"title": "Hacked"}, format="json")
        self.assertEqual(response.status_code, status.HTTP_403_FORBIDDEN)

    def test_delete_product_owner(self):
        self.client.force_authenticate(user=self.user)
        url      = reverse("product-detail", kwargs={"pk": self.product.pk})
        response = self.client.delete(url)
        self.assertEqual(response.status_code, status.HTTP_204_NO_CONTENT)
        self.assertEqual(Product.objects.count(), 0)
```

```bash
# Run all tests
python manage.py test

# Run tests for a specific app
python manage.py test users

# Run a specific test class
python manage.py test users.tests.ProductAPITest

# Run a specific test method
python manage.py test users.tests.ProductAPITest.test_create_product_authenticated

# Run with verbose output
python manage.py test --verbosity=2

# Run with coverage
pip install coverage
coverage run manage.py test
coverage report
coverage html   # generates a visual HTML report in htmlcov/
```

---

## Security Best Practices

Django comes with many security features built in. You just need to know how to turn them on properly.

```python
# settings.py for production
DEBUG = False   # NEVER set this to True in production

SECURE_SSL_REDIRECT            = True
SECURE_HSTS_SECONDS            = 31536000     # 1 year
SECURE_HSTS_INCLUDE_SUBDOMAINS = True
SECURE_HSTS_PRELOAD            = True

SESSION_COOKIE_SECURE  = True   # send cookies over HTTPS only
CSRF_COOKIE_SECURE     = True
SESSION_COOKIE_HTTPONLY = True  # prevent JavaScript from reading the session cookie
X_FRAME_OPTIONS        = "DENY" # clickjacking protection
```

```python
# SQL injection -- the ORM prevents this automatically
# Never do string formatting with user input in raw queries
User.objects.raw(f"SELECT * FROM users WHERE email = '{user_input}'")  # DANGEROUS!

# Always use parameterized queries if you must use raw SQL
User.objects.raw("SELECT * FROM users WHERE email = %s", [user_input])  # safe

# XSS -- Django templates auto-escape HTML output by default
# {{ user_input }} is always safe because Django escapes it
# {{ user_input|safe }} turns escaping OFF -- only use when you are 100% certain

# Password validation
AUTH_PASSWORD_VALIDATORS = [
    {"NAME": "django.contrib.auth.password_validation.UserAttributeSimilarityValidator"},
    {"NAME": "django.contrib.auth.password_validation.MinimumLengthValidator",
     "OPTIONS": {"min_length": 8}},
    {"NAME": "django.contrib.auth.password_validation.CommonPasswordValidator"},
    {"NAME": "django.contrib.auth.password_validation.NumericPasswordValidator"},
]
```

---

## Performance Optimization

```python
# 1. The most common problem: N+1 queries
# BAD: 1 query for products, then 1 extra query per product for its category
products = Product.objects.all()
for product in products:
    print(product.category.name)   # hits the database on EVERY iteration!

# GOOD: single query with JOIN
products = Product.objects.select_related("category").all()
for product in products:
    print(product.category.name)   # no extra queries, data already loaded

# GOOD: use prefetch_related for ManyToMany and reverse FK
products = Product.objects.prefetch_related("tags").all()

# 2. Only fetch the columns you need
User.objects.values("id", "email")       # dictionary output, much faster
User.objects.only("id", "email")         # model instances but fewer columns
User.objects.defer("bio", "avatar")      # load everything EXCEPT these fields

# 3. Add indexes on fields you filter or sort on often
class Product(models.Model):
    class Meta:
        indexes = [
            models.Index(fields=["status", "created_at"]),
            models.Index(fields=["slug"]),
        ]

# 4. Use exists() instead of count() when you just need a yes/no answer
if Product.objects.filter(status="published").exists():   # faster
    pass

# 5. Bulk operations instead of looping
Product.objects.bulk_create([
    Product(title="Phone",  price=499),
    Product(title="Tablet", price=299),
])
Product.objects.bulk_update(products, ["price", "stock"])

# 6. Always paginate list endpoints, never return the full table
from rest_framework.pagination import PageNumberPagination

class StandardPagination(PageNumberPagination):
    page_size              = 20
    page_size_query_param  = "page_size"
    max_page_size          = 100

# 7. Use iterator() for large querysets to avoid loading everything into memory at once
for product in Product.objects.iterator(chunk_size=500):
    process(product)

# 8. Install django-debug-toolbar during development to spot slow queries visually
# pip install django-debug-toolbar
```

---

## Deployment

```bash
# Install production dependencies
pip install gunicorn psycopg2-binary whitenoise

# Collect static files
python manage.py collectstatic --noinput

# Apply database migrations
python manage.py migrate

# Start Gunicorn (4 worker processes)
gunicorn myproject.wsgi:application --bind 0.0.0.0:8000 --workers 4
```

```python
# settings/production.py
# WhiteNoise serves static files directly from Django without needing nginx for static
MIDDLEWARE = [
    "django.middleware.security.SecurityMiddleware",
    "whitenoise.middleware.WhiteNoiseMiddleware",   # must be right after Security
    ...
]

STORAGES = {
    "staticfiles": {
        "BACKEND": "whitenoise.storage.CompressedManifestStaticFilesStorage",
    },
}
```

```dockerfile
# Dockerfile
FROM python:3.12-slim

WORKDIR /app

COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

COPY . .
RUN python manage.py collectstatic --noinput

EXPOSE 8000
CMD ["gunicorn", "myproject.wsgi:application", "--bind", "0.0.0.0:8000", "--workers", "4"]
```

```yaml
# docker-compose.yml
version: "3.8"
services:
  web:
    build: .
    ports:
      - "8000:8000"
    env_file:
      - .env
    depends_on:
      - db
      - redis

  db:
    image: postgres:16
    environment:
      POSTGRES_DB:       myapp
      POSTGRES_USER:     myuser
      POSTGRES_PASSWORD: mypassword
    volumes:
      - postgres_data:/var/lib/postgresql/data

  redis:
    image: redis:7-alpine

  celery:
    build: .
    command: celery -A myproject worker --loglevel=info
    env_file:
      - .env
    depends_on:
      - db
      - redis

volumes:
  postgres_data:
```

---

## Common Interview Questions

### Q1. What is Django and what makes it different from Flask?
Django is a batteries-included Python web framework that comes with an ORM, admin panel, authentication, forms, and much more out of the box. Flask is a micro-framework that gives you just the basics and lets you choose your own tools for everything else. Django is the better choice when you need a full-featured production application fast and want things like an admin panel without building it yourself. Flask works well when you want full control over your stack and are building something smaller or very specific.

### Q2. Explain the Django request response cycle.
When a request comes in it first passes through all middleware in order, where each layer can modify the request or block it early. Django then matches the URL against patterns in `urls.py` and calls the matched view. The view does its work, querying the database through the ORM and building a context. The view returns a response which passes back through the middleware in reverse order before going back to the browser. If anything raises an exception along the way, Django's exception handling and any custom error views kick in.

### Q3. What is the Django ORM and what are its advantages?
The ORM (Object-Relational Mapper) lets you interact with your database using Python code instead of writing raw SQL. Instead of writing `SELECT * FROM products WHERE status = 'published'` you write `Product.objects.filter(status='published')`. The main advantages are automatic SQL injection prevention, database agnosticism (you can switch from SQLite to PostgreSQL without changing your Python code), and keeping everything in one language. For very complex queries you can drop down to raw SQL when needed.

### Q4. What is the N+1 query problem and how do you fix it?
The N+1 problem happens when you load a list of objects with one query and then access a related object on each of them, which fires one extra query per object. For 100 products each with a category that becomes 101 database queries instead of 1. You fix it with `select_related()` for ForeignKey and OneToOne relationships which adds a SQL JOIN, and `prefetch_related()` for ManyToMany and reverse FK which runs a second separate query and joins the results in Python. During development the `django-debug-toolbar` package shows you all queries on each page so you can spot these problems instantly.

### Q5. What is the difference between `null=True` and `blank=True`?
`null=True` tells the database that the column can store a NULL value at the database level. `blank=True` tells Django's form validation that the field is allowed to be empty in forms and the API. For string-based fields like `CharField` and `TextField` you should use only `blank=True` and not `null=True` because Django stores empty strings for text, not NULL, so having both creates two possible representations of "no value." For non-string fields like `DateField`, `ForeignKey`, or `IntegerField` you use both `null=True, blank=True` to make the field truly optional.

### Q6. What are Django signals and when should you use them?
Signals are Django's way of letting different parts of your app communicate when events happen without them being directly connected. For example `post_save` fires every time any model instance is saved. Common real-world uses are auto-creating a user profile when a user registers, sending a welcome email after signup, or clearing a cache when related data changes. The downside is that signal connections are implicit, making code harder to follow and test. A good rule of thumb is to use signals for true side effects that are separate from the main action, and to override `save()` for logic that is directly tied to the model itself.

### Q7. What is the difference between `select_related` and `prefetch_related`?
`select_related` works with ForeignKey and OneToOne relationships. It adds a SQL JOIN to the original query and fetches the related data in the same database round trip. `prefetch_related` works with ManyToMany and reverse ForeignKey relationships. It runs a second separate query and then Python handles the joining in memory. The rule is: use `select_related` when traversing to a single related object (like a product's category), and `prefetch_related` when traversing to multiple related objects (like a product's tags or a user's orders).

### Q8. How do Django migrations work?
Migrations are Python files that track every change to your models over time. When you change a model you run `makemigrations` which generates a new migration file describing the change in a format Django can apply or reverse. Then you run `migrate` which actually executes the SQL on your database and records in a special `django_migrations` table which migrations have already been applied. This system lets your database schema evolve safely over time with a full history and the ability to roll back.

### Q9. What are class-based views and when would you use them over function-based views?
Class-based views are reusable view classes that handle common patterns. Django's generic views like `ListView`, `DetailView`, `CreateView`, `UpdateView`, and `DeleteView` give you complete CRUD functionality with very little code. They also support mixins for adding behavior like login requirements. Function-based views are simpler and more explicit which can make them easier to read and debug. A practical guideline is to use generic CBVs when your view fits one of the standard patterns cleanly, and to use FBVs when you have custom logic that does not map naturally to a generic view.

### Q10. What is DRF and what are its core components?
DRF (Django REST Framework) is the standard package for building REST APIs with Django. Its core components are Serializers (convert model instances to JSON and validate incoming data), ViewSets (combine list/create/retrieve/update/delete logic into one class), Routers (auto-generate URL patterns from ViewSets), Permissions (control who can access which endpoints), Authentication (JWT, session, token), and Throttling (rate limiting). Together they give you a full API toolkit with very little boilerplate code.

### Q11. What is a serializer in DRF and how is it similar to a Django form?
Both serializers and forms validate incoming data and convert it into a clean, usable format. A Django form validates HTML form submissions and can render HTML form fields. A DRF serializer validates incoming JSON data and converts model instances into JSON for API responses. Serializers also handle nested relationships and can use different representations for read vs write operations. In practice you almost always use `ModelSerializer` which auto-generates fields from your model, very similar to how `ModelForm` works for HTML forms.

### Q12. How do you handle authentication in a Django REST API?
The most common approach for modern APIs is JWT using `djangorestframework-simplejwt`. The login endpoint returns a short-lived access token (typically 15 minutes) and a longer-lived refresh token (typically 7 days). The client sends the access token as a `Bearer` header on every API request. When the access token expires the client uses the refresh token to get a new one silently without the user needing to log in again. DRF's authentication classes verify this token on every request and populate `request.user` automatically.

### Q13. What is Celery and why would you use it with Django?
Celery is a task queue that lets you run code asynchronously in the background, outside of the normal request response cycle. You use it for anything that is slow or resource-heavy and would make the user wait unnecessarily, like sending emails, processing uploaded images, generating PDF reports, calling slow third-party APIs, or running scheduled recurring jobs. Without Celery, a view that sends an email might take 3 or 4 seconds to respond. With Celery you push the work to a background worker and respond instantly, then the email goes out in the background.

### Q14. How does caching work in Django and when would you use it?
Django has a caching framework with multiple backends including Redis and Memcached. You can cache at the full view level using `@cache_page`, at the template fragment level using the `{% cache %}` tag, or at the code level using the low-level cache API. You would use caching for data that is expensive to compute but does not change often, like a featured products list, a leaderboard, category trees, or aggregated statistics. The trickiest part of caching is invalidation which means making sure you clear the cached value when the underlying data changes so users never see stale data.

### Q15. What are the most important things to check before deploying a Django app to production?
Set `DEBUG = False` because debug mode exposes sensitive information including full stack traces in the browser. Set `ALLOWED_HOSTS` to only your actual domain. Switch from SQLite to PostgreSQL. Move all secrets and keys to environment variables and never hardcode them. Enable all HTTPS security settings including `SECURE_SSL_REDIRECT`, `SESSION_COOKIE_SECURE`, and `CSRF_COOKIE_SECURE`. Run `collectstatic` and serve static files through WhiteNoise or a CDN. Apply all pending migrations before starting the server. Set up logging so you have visibility into what is happening. Use Gunicorn or uWSGI instead of Django's development server, and ideally put nginx in front of it for SSL termination and serving media files.

---

## Contributing

Found a mistake or want to add something? Open a PR or raise an issue. All contributions are welcome.

---

## Author

**Haseeb Javed**
Full-Stack Developer | React, Next.js, TypeScript, NestJS, Django, FastAPI

- GitHub: [@haseebjaved4212](https://github.com/haseebjaved4212)
- Email: contactimhaseeb@gmail.com

---

## License

This project is open source and available under the [MIT License](LICENSE).