## Configuraciones:

### views.py 
 Existen varios tipos de vistas, entre ellas:
	[[101 apiViews|apiViews:]] Son vistas básicas similares a las vistas tradicionales que existen en django, usa el archivo de urls tradicional, mientras las viewsets usan un router
```python
	class HelloApiView(APIView):
```

  [[102 viewSets|viewSets:]] En las viewsets no se personalizan rutas si no routers. La diferencia con las apiviews y genericviews, es que para listar un objeto, actualizarlo o eliminarlo; la URL está esperando un parametro como pk para saber a cual se quiere acceder, mientras en las apiviews se debe hacer rutas por cada verbo HTTP
	
```python
class EstadoConstruccionViewSet(ViewSet):
	model = EstadoConstruccion
	
	def list(self, request):
		data = self.model.objects.filter(estado=True)
		data = self.serializer_class(data, many=True)
		return Response(data.data, status=status.HTTP_200_OK)
```

### serializerls.py
```python
class EstadoContruccionSerializer(serializers.ModelSerializer): 

	class Meta: 
		exclude = ('estado', )
```
Acá irán los modelos que se renderizaran en el navegador como JSON, a este proceso se le conoce como serializar. Existen varios tipos de serializadores:

#### [[201 serializando_funciones|Serializando funciones]]
#### [[202 serializando_classes|Serializando clases]]
#### [[203 serializando_array|Serializando arrays]]
#### [[204 serializando_foreing_key|Serializando Foreing Keys]]

### urls.py - Global
```python
from django.contrib import admin
from django.urls import path, include

urlpatterns = [
	path('admin/', admin.site.urls),
	path('api/products/', include('apps.products.api.routers'))
]
```

### urls.py   - app
- Cuando se usan vistas basadas en funciones,  se deben configurar las [[300 urls#Basadas en funciones|urls basadas en funciones]] en el archivo urls.py de la aplicación.
- Cuando se usan las [[103 genericApiViews|vistas genéricas]], se deben configurar las [[300 urls#Basadas en genericViews|urls basadas en genericViews]] en el archivo urls.py de la aplicación. 
- Cuando se usan las vistas basadas en [[102 viewSets|viewsets]] se configuran en el archivo [[300 urls#Basadas en viewsets|router.py]]
 
### models.py
 En este archivo irán los modelos correspondientes a la aplicación
```python
class EstadoConstruccion(ModeloBase): # Hereda de un modelo base
	"""Model definition for EstadoConstruccion.""" 
	nombre_estado_construccion = models.CharField(
		verbose_name='Nombre del estado de contrucción', max_length=100
		) 
	historial = HistoricalRecords() 
```
  > _[[400 models.py|Más]]_
  