
## Basic  Manager: 
```python
import django.db import models

class UserManager(models.Manager):

	def list_users(self):
		return self.all()
```

#### On the views file , it changes the return of the get_queryset method for the new consult:
```python
from django.views.generic import ListView
from .models import User

class ListUsers(ListView):
	context_object_name = 'list_users'
	template_name = 'user/list.html'

	def get_queryset(self):
		return User.objects.list_users() # Manager create from UserManager
```

#### Connect model with manager:
```python
import django.db import models

class User(models.Model):
# custom fields...
objects = UserManager()
```

## Manager Filters

#### Simple filters:
```python
import django.db import models

class UserManager(models.Manager):

	def search_users(self, key_word):
		result = self.filter(field__icontains=key_word)
		return result
```

#### Or filters:
```python
from django.db import models
from django.db.models import Q

class UserManager(models.Manager):

	def search_users(self, key_word):
		result = self.filter(
			Q(field__icontains=key_word) | Q(field2__icontains=key_word)
			)
		return result
```

#### Exclution filters:
```python
from django.db import models
from django.db.models import Q

class UserManager(models.Manager):

	def search_users(self, key_word):
		result = self.filter(field__icontains=key_word).exclude(field2=value)
			)
		return result
```

#### grather than, lower than filters:
```python
from django.db import models
from django.db.models import Q

class UserManager(models.Manager):

	def search_users(self, key_word):
		result = self.filter(
			field__gt=number, field__lt=number
			).order_by('field')
		
		return result
```

#### dates:
```python
from django.db import models
from django.db.models import Q

class UserManager(models.Manager):

	def search_users(self, key_word):
		result = self.filter(
			field__gt=number, 
			date_field__range=('yyyy-mm-dd', 'yyyy-mm-dd')
			)
		
		return result

# Date ranges from html
import datetime
def range_date(self, key_word, initial_date, final_date):

	date1 = datetime.datetime.strptime(initial_date, "%Y-%m-%d").date()
	date2 = datetime.datetime.strptime(final_date, "%Y-%m-%d").date()
	
	result = self.filter(
		field__gt=number, 
		date_field__range=(date1, date2)
		)
		# On the views validate if date are not empty
		# if initial_date and final_date:
			# return User.objects.range_date(key_word, initial_date, final_date)
		# else:
			# return User.objects.another_consult
	
	return result
```

## Relations

#### Many to One:
```python
import django.db import models

class UserManager(models.Manager):

	def list_category(self, category):
		result = self.filter(category__id=category).order_by('field')
		return result
```

#### Many to Many: Related name
```python 
	# models.py

class Book(models.Model):
	Category = models.ForeingKey(
		Category,
		on_delete=models.CASCADE,
		related_name='category_book' # Relative name
	)
```
```python
	# managers.py
import django.db import models

class CategoryManager(models.Manager):

	def list_category(self, user):
		result = self.filter(category_book__Users__id=user).distinct()
		return result
```

- Many to Many:
	```django

	<ul>
		{% for author in libro.authors.all %}
		<li> {{ author }} </li>
		{% endfor %}
	</ul>
	```

## Arithmetic

#### Annotate
arithmetic query -> returns a queryset
```python
import django.db import models
from django .db.models import Count

class UserManager(models.Manager):

	def list_category(self):
		result = self.annotate(
			num_books=Count(related_name)
		)			
		return result
```

#### Agregate
arithmetic query  -> returns a python dict
```python
import django.db import models
from django .db.models import Count, Avg, Sum

class UserManager(models.Manager):

	def user_count(self):
		result = self.aggregate(
			num_books=Count(related_name)
		)			
		return result

	def user_avg(self):
		result = self.filter(
			user__id=num_id
		).aggregate(
			avg_age=Avg('field_foreign_key__field',
			sum_age=Sum('field_foreign_key__field')
		)
		return result
```

#### Group_by:  -> returns a python dict
```python
import django.db import models
from django .db.models import Count, Avg, Sum
from django .db.models.functions import Lower

class UserManager(models.Manager):

	def book_group_count(self):
		result = self.values(
			'field_foreign_key',
			'query_2'
		).annotate(
			num_books=Count(related_name),
			title=Lower('field_foreign_key__field')
		)			
		return result
```

#### Trigram
First register postgres app : 'django.contrib.postgres'
```python

import django.db import models
from django .db.models import Count, Avg, Sum
from django .db.models.functions import Lower

class UserManager(models.Manager):

def list_books_trg(self, kword):

	if kword:
		result = self.filter(
			title__trigram_similar=kword,
		)			
		return result
	else:
		return self.all()[:10]	
	```

#### Custom admin django 
```python
import django.db import models
from django.contrib.auth.models import AbstractBaseUser, BaseUserManager

class UserManager(BaseUserManager):
	def create_user(
		self, 
		email,
		username, 
		nombre, 
		apellido, 
		password=None
	):
		if not email:
			raise ValueError('User must have an email')

		user = self.model(
			username=username,
			email = self.normalize_email(email),
			name = name,
			lastname = lastname
		)

		user.set_password(password)
		user.save(using=self.db)
		return user

		def create_superuser(
			self, 
			email,
			username, 
			nombre, 
			apellido, 
			password
		):
			user = self.create_user(
				email,
				username=username,
				name=name,
				lastname=lastname,
				password=password
			)
			user.administrator = True
			user.save()
			return user

class User(models.Model):
	# custom fields...
	objects = UserManager()

	USERNAME_FIELD = 'username' # Indicates which field will be used to validate
	REQUIRED_FIELDS = ['email', 'nombre'...] # Required fields for the creation of a new user

	def __str__(self):
		return f'{self.field}'

	def has_perm(self, perm, obj=None):
		return True

	def has_module_perms(self, app_label):
		return True

	@property
	def is_staf(self): => Retorna si el usuario es o no admin
		return self.usuario_admin

	 '''
		In the settings file put the configuration so that it recognizes
		you as the new user
	'''

AUTH_USER_MODEL = 'nombre_app.nombre_model'
```

