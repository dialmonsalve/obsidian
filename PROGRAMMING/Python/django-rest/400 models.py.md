```python
class EstadoConstruccion(ModeloBase): # Hereda de un modelo base
	"""Model definition for EstadoConstruccion.""" 
	nombre_estado_construccion = models.CharField(
		verbose_name='Nombre del estado de contrucción', max_length=100
		) 
	historial = HistoricalRecords() 
	
	@prperty 
	def _history_user(self): 
		return self.changed_by 
	
	@_history_user.setter 
	def _history_user(self, value): 
		return self.value class Meta: 
		"""Meta definition for EstadoConstruccion""" 
		
		verbose_name = 'Estado de la contruccion' 
		verbose_name_plural = 'Estados de la contruccion' 
		
	def __str__(self): 
	"""Unicode representation of EstadoConstruccion""" 
		return self.nombre_estado_construccion
```