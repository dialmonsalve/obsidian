
## Based on functions - Classes

- This file shows how the configuration of the apps file should be, both for views based on classes and functions
	```python
	from django.apps import AppConfig 

	class PageConfig(AppConfig): 
		default_auto_field = 'django.db.models.BigAutoField' 
		name = 'pages'
	```
