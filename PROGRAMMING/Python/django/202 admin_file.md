
## Based on functions - Classes

- This file shows how the configuration of the admin file should be, both for views based on classes and functions
	```python
	from django.contrib import admin
	from .models import Category, Author

		class CategoryAdmin(admin.ModelAdmin):
			search_fields = ['name']
			list_display= ('name', 'state', 'create_at', 'full_name',  )
												# Field full_name doesn't exist

			def full_name(self, obj): # Create custom fields    
			 return f'{obj.name}  {obj.create_at} '
		
		class AuthorAdmin(admin.ModelAdmin):
			search_fields = ['name', 'lastname', 'email',]
			list_display= ('name', 'lastname', 'email', 'state','create_at', )

		# Register your models here.
		admin.site.register(Category, CategoryAdmin)
		admin.site.register(Author, AuthorAdmin)
	```
