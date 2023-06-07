#### ViewSet : ViewSet genérica
Se pueden sobrescribir los métodos get, post, put, patch y delete pero las viewsets trabajan con métodos basados en acciones (list, retrieve, create,  update, partial_update y destroy)
mas: [ViewSets](https://www.cdrf.co/3.13/rest_framework.viewsets/ViewSet.html) en www.cdrf.co
```python
	from rest_framework import APIView,viewSets, status
	from rest_framework.response import Response

	from . import serializers

	class HelloViewSet(viewSets.ViewSet):

		serializer_class = serializers.HelloSerializer
	
		# MÉTODO GET		
		def list(self, request):
			an_viewset = [
				'Metodos http usados como acciones(list, create, retrieve, partial_update, destroy)',
				'Mapea automaticamente urls usando routers',
				'Proveé mas funcionalidades con código mas simple',
			]
			return Response({'message': 'hello', 'an_viewset': an_viewset})

		# MÉTODO POST
		def create(self, request):
			serializer = self.serializer_class(data=request.data)

			if serializer.is_valid():
				name = serializer.validated_data.get('name')
				message = f'Hello {name}'
				return Response({'message': message})
			else:
				return Response(
					serializer.errors, 
					status=status.HTTP_400_BAD_REQUEST
				)

		# MÉTODO GET UN POR ID
		def retrieve(self, request, pk=None):
			return Response({'method': 'GET'})
			
		# MÉTODO PUT
		def update(self, request, pk=None):
			return Response({'method': 'PUT'})
			
		# MÉTODO PATCH
		def partial_update(self, request, pk=None):
			return Response({'method': 'PATCH'})
			
		# MÉTODO DELETE
		def destroy(self, request, pk=None):
			return Response({'method': 'DELETE'})
			

```

Cambiando permisos con un viewSet según action
```python
class VentasViewSet(viewsets.viewSet):
	authentication_calsses = (TokenAuthentication,)
	queryset  = Sale.objects.all()

	def get_persmision(self):
		if (self.action=='list'):
			permission_classes = [AllowAny] # importar
		else
			permission_classes = [IsAuthenticated]

		return [permission() for permission in permission_classes]

	def create(self, request):
		...
		return Response({'code':'ok'})

	....
```

#### ModelViewSet
Está diseñado para trabajar con los modelos y proporciona acciones y comportamientos predefinidos para realizar operaciones comunes en el modelo
```python
from rest_framework import status
from rest_framework.response import Response
from rest_framework import viewsets

from apps.products.api.serializers.products_serializers import ProductSerializer

class ProductViewSet(viewsets.ModelViewSet):
	serializer_class = ProductSerializer
	
	def get_queryset(self, pk=None):
		if pk is None:
			return self.get_serializer().Meta.model.objects.filter(state=True)
		return self.get_serializer().Meta.model.objects.filter(id=pk, state=True).first()
	
	def create(self, request):
		serializer = self.serializer_class(data = request.data)
		if serializer.is_valid():
			serializer.save()
			return Response(
				{'message': 'Producto creado correctamente'}, 
				status=status.HTTP_201_CREATED)
		return Response(
				serializer.errors, 
				status=status.HTTP_400_BAD_REQUEST)
		
	def update(self, request, pk=None, *args, **kwargs, ):
		if self.get_queryset(pk):
			product_serializer = self.serializer_class(self.get_queryset(pk), data = request.data)
			if product_serializer.is_valid():
				product_serializer.save()
				return Response(product_serializer.data, status=status.HTTP_200_OK)
		return Response(product_serializer.errors, status=status.HTTP_400_BAD_REQUEST)
	
	def destroy(self, request, pk = None):
		product = self.get_queryset().filter(id = pk).first()
		if product:
			product.state = False
			product.save()
			return Response(
				{'message': 'Producto eliminado correctamente'}, 
				status=status.HTTP_200_OK)
		return Response(
				{'message': 'No existe un producto con estos datos'}, 
				status=status.HTTP_400_BAD_REQUEST)
```