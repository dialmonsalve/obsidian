
## Based on functions - Classes

This file shows how the configuration of the models file should be, both for views based on classes and functions    
```python
from django.db import models

class Model(models.Model):
	name = models.CharField(verbose_name="Name", blank=False)
	email= models.EmailField(verbose_name="Email", null=False)
	content = models.CharField(verbose_name="Content", max_length=250 )

	class Meta:
		verbose_name = 'Model'
		verbose_name_plural = 'Models'
		ordering = ['name', ]
		db_table = 'name' # Real table name inside database
		unique_together = ['field1', 'field2'] # Not allows registers with thesse two combinations
		constraints =[ # Restrictions
			models.CheckContrainst(
				check=models.Q(
					age__gte=18
				), name='age_over_18'
			)
		]
		abstract = True # It is a model, but it doesn't create a table in the db

	#Manera para mostrar el nombre en la tabla admin.Default es: object(Object)
	def __str__(self):
		return self.name
```