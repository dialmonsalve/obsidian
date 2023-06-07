
#### **models.CharField()**
This field is used to specify strings properties
- **Param:**
	- max-length(_num_): It specify the numbers of characters
	- blank(_bool_): True if you want the field accept empty values 
	- Choices(_str[]_) 
```python
	class Author(models.Model):
		full_name = models.CharField(max_length=60)
		addresse = models.CharField(max_length=80, blank=True)
		gender = models.CharField(max_length=80, choices=array_choices)
```

#### **models.BooleanField()**
This field is used to specify if the field is true or false properties
- **Param:**
	- blank(_bool_): True if you want the field accept empty values 
	- default(_bool_): It specifies if the field uses a default value
```python
	class Book(models.Model):
		title = models.CharField(max_length=60)
		published = models.BooleanField(default=False)
```
 
#### **models.DateField():**
This field is used to specify if the field is true or false properties
- **Param:**
	- null(_bool_): It specifies a boolean if accepts null values
	- default(_bool_): It specifies if the field uses a default value
	- auto_now(_bool_):  Field for model update date
```python
	class Book(models.Model):
		titulo = models.CharField(max_length=60)
		published = models.BooleanField(default=False)
		create_published = models.DateField(null=False, auto_now=True)
```
 
#### **models.DateTimeField():**
This field is used to specify if the field is true or false properties, besides the hours
```python
class Book(models.Model):
	titulo = models.CharField(max_length=60)
	published = models.BooleanField(default=False)
	create_published = models.DateTimeField(null=False, auto_now=True)
```

#### **models.EmailField():**
This field is used to specify email validation values
```python
	class Author(models.Model):
		full_name = models.CharField(max_length=60)
		email = models.EmailField(blank=True)
```

#### **models.URLField():**
This field is used to specify URL validation values
```python
	class Author(models.Model):
		full_name = models.CharField(max_length=60)
		email = models.EmailField(blank=True)
		profile = models.URLField(null=True)
```

#### **models.ImageField():**
This field is used to upload and save images on the server
 - **Param:**
	- upload(_str_): It specifies a string with a URL path where the image is saved 
```python
	class Author(models.Model):
		full_name = models.CharField(max_length=60)
		email = models.EmailField(blank=True)
		profile = models.URLField(null=True)
		image = models.ImageField(null=True, upload='/static/photos')
```

#### **models.PositiveIntegerField():**
This field is used to specify a positive number, it is useful when the fields are ages
 - **Param:**
	- upload(_str_): It specifies a string with a URL path where the image is saved 
```python
class Author(models.Model):
	full_name = models.CharField(max_length=60)
	email = models.EmailField(blank=True)
	profile = models.URLField(null=True)
	image = models.ImageField(null=True, upload=’fotos’)
	age = models.PositiveIntegerField(default=0)
```
