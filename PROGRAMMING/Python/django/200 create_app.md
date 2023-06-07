
### Create a new app

####  1. Command new app
```shell
python manage.py startapp name_ap
django-admin startapp name_ap # Se usa cuando no se tiene acceso directo al
manage.py
```

#### 2. Create the new app view
```python
from django.shortcuts import render
def name(request):
	return render(request, "root/page.html")
```

#### 3. Create and Configure the new global urls file
```python
#Based on metods:
from django.urls import path, include

urlpatterns = [
	path('root/', include('app.urls')),
]

#Based on classes:
from django.contrib import admin
from django.urls import path, include
from pages.urls import pages_patterns

urlpatterns = [
	path('pages/', include(pages_patterns)),
	path('admin/', admin.site.urls),
]
```

#### 4. Add the new app inside settings file
```python
INSTALED_APPS = [
	"app"
]
```

- **Note:** When we want to use a custom configuration in the admin file, on settings file it must configure the app as follows
	```python
	INSTALED_APPS = [
		"name_app.apps.Congiguracion"
	]
	```

#### 5. Crearte the template directory