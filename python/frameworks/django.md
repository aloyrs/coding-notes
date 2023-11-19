Django is a high-level web framework for building web applications quickly and efficiently. It follows the Model-View-Controller (MVC) architectural pattern . (Python backend framework)

# Install Django

```bash
pip install django
```

# Create a Django Project

```bash
django-admin startproject projectname
cd projectname
```

# Create a Django App

```bash
python manage.py startapp appname
```

# Configure Database

Open `settings.py` in your project folder and configure the database settings under the `DATABASES` section.

```python
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.sqlite3',
        'NAME': BASE_DIR / "db.sqlite3",
    }
}
```

# Create Models

Edit the `models.py` file in your app to define your data models.

```python
from django.db import models

class YourModel(models.Model):
    field1 = models.CharField(max_length=100)
    field2 = models.IntegerField()

    def __str__(self):
        return self.field1
```

# Make Migrations

Run the following commands to create and apply database migrations:

> Migrations are how Django stores changes to your models , by running `makemigrations` , you're telling Django that you have made changes in models and want changes stored as migration

```bash
python manage.py makemigrations
python manage.py migrate
```

# Create Admin Panel (Optional)

In your app's `admin.py`, register your models to make them accessible in the admin panel.

```python
from django.contrib import admin
from .models import YourModel

admin.site.register(YourModel)
```

# Create Views and Templates

Create views in your app's `views.py` and corresponding HTML templates in the `templates` folder.

`views.py` : Handle request and return response

## `path()` function

> Two required: **route** and **view**, and two optional: **kwargs**, and **name**

> route : `polls/` will lead to `http://127.0.0.1:8000/polls/`

> view :

> kwargs :

> name : provide unique name for url where you can refer in whole project

# Configure URLs

> Handles routing

In your app's `urls.py`, define the URL patterns for your views.

Include these patterns in the project's `urls.py` using `include()` in the `path()` function.

## Run the Development Server

```bash
python manage.py runserver
```

Visit `http://127.0.0.1:8000/` in your browser to see your Django app in action.
