#### 1.  **Create**
In the directory app one directory named templates, inside another directory called registration. Inside registration create all native Django templates

#### 2.  **Register** 
the new app on the first line inside the settings.py file and set the variables for the new login
```python
INSTALED_APPS = [
	'registration',
	"app"
]

# Final line
LOGIN_REDIRECT_URL = 'home'
LOGOUT_REDIRECT_URL = 'login'
```

#### 3.  **Configure**
the global urls 
```python
from django.contrib import admin
from django.urls import path, include

urlpatterns = [ 
	path('admin/', admin.site.urls),

	# Paths de auth
	path('accounts/', include('django.contrib.auth.urls')),
	path('accounts/', include('registration.urls')),
]
```

#### **Register** users
-   On the **view.py**
	```python
	from djang.contrib.auth.forms import UserCreationForm
	from djang.views.generic import CreateView
	from django.urls import reverse_lazy
	from .models import Model
	from .forms import InstanceForm 
	
	class SignUpView(CreateView):
		form_class = UserCreationForm # Formulario de admin Django
		success_url = reverse_lazy('login')
		template_name = 'registration/signup.html' #Crear la vista	
	```

-   On the **urls.py**
	```python
	from django.urls import path
	from .views import SignUpView, 
	  
	pages_patterns = ([
			path('signup/', SignUpView.as_view(), name='signup'),
	], 'pages')
	```
 
#### **Restore** passwords 
URL: localhost:8000/accounts/template.html

On the directory registration/templates/registration/create the Django templates 

password_reset_complete.html    
password_reset_confirm.html    
password_reset_done.html    
password_reset_form.html

#### **Create** profiles
To add extra fields in the user profile it could be done in two ways

##### 1. **Extend** Django's default user with a 1:1 relationship        
```python
from django.contrib.auth.models import User
from django.db import models

class Profile(models.Model):
	user = models.OneToOneField(User, on_delete=models.CASCADE)
	campos adicionales
```

###### 2. **Create** a new user by overwriting  the Django user with [[404 query_managers#Custom admin django|Managers]]

#### **Change** passwords
Create the password_reset.html and password_reset_done.html templates
