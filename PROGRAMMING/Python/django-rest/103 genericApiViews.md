### GenericApiViews
Esta vista no permite sobrescribir los métodos HTTP (get, put, patch, delete)
mas: [GenericApiViews](https://www.cdrf.co/3.13/rest_framework.generics/GenericAPIView.html) en www.cdrf.co

### CreateApiView
Esta vista permite sobrescribir los métodos post y create; entre otros.
mas: [CreateApiView](https://www.cdrf.co/3.13/rest_framework.generics/CreateAPIView.html) en www.cdrf.co
```python
from rest_framework import generics, status
from rest_framework.response import Response

from apps.base.api import GeneraListApiView
from apps.products.api.serializers.products_serializers import ProductSerializer
from apps.products.models import Product 

class ProductCreateAPIView(generics.CreateAPIView):
	serializer_class = ProductSerializer
	
	def post(self, request):
		serializer = self.serializer_class(data = request.data)
		if serializer.is_valid():
			serializer.save()
			return Response(
				{'message': 'Producto creado correctamente'}, 
				status=status.HTTP_201_CREATED)
		return Response(
				serializer.errors, 
				status=status.HTTP_400_BAD_REQUEST)
		
	def create(self, validated_data):
		if validated_data['image'] == None:
			validated_data['image'] = ''
		return Product.objects.create(**validated_data)
```

### ListApiView
Esta vista permite sobrescribir los métodos get y list; entre otros.
mas: [ListApiView](https://www.cdrf.co/3.13/rest_framework.generics/ListAPIView.html) en www.cdrf.co
```python
from rest_framework import generics, status
from rest_framework.response import Response

from apps.base.api import GeneraListApiView
from apps.products.api.serializers.products_serializers import ProductSerializer
from apps.products.models import Product 

class Listproduct(ListApiView):
	serializer_class = ProductSerializer # Recibir por ulr

	def get_queryset(self):
		gender = self.kwargs['gender']
		return Product.objects.manager_class(gender)

class Filterproduct(ListApiView):
	serializer_class = ProductSerializer # Recibir por ulr

	def get_queryset(self):
		man = self.request.query_params.get('man', None)
		woman = self.request.query_params.get('woman', None)
		name = self.request.query_params.get('name', None)

		return Product.objects.filter_products(
			man=man,
			woman=woman,
			name=name
		)

#Create a method inside the Manager
class ....
	
	def filter_products(self, **kwargs):
		return self.filter(
			man=kwargs['man'],
			woman=kwargs['woman'],
			name__icontains=kwargs['name'],
		)

```

### RetrieveAPIView
Esta vista permite sobrescribir los métodos get, entre otros.
mas: [RetrieveAPIView](https://www.cdrf.co/3.13/rest_framework.generics/RetrieveAPIView.html) en www.cdrf.co
```python
from rest_framework import generics, status

from apps.products.api.serializers.products_serializers import ProductSerializer

class ProductRetrieveAPIView(generics.RetrieveAPIView):
	serializer_class = ProductSerializer
	
	def get_queryset(self):
		return self.get_serializer().Meta.model.objects.filter(state=True)
```

### UpdateAPIView
Esta vista permite sobrescribir los métodos put, patch , entre otros.
mas: [UpdateAPIView](https://www.cdrf.co/3.13/rest_framework.generics/UpdateAPIView.html) en www.cdrf.co
```python
from rest_framework import generics, status
from rest_framework.response import Response

from apps.base.api import GeneraListApiView
from apps.products.api.serializers.products_serializers import ProductSerializer
from apps.products.models import Product 

class ProductUpdateAPIView(generics.UpdateAPIView):
	serializer_class = ProductSerializer
	
	def get_queryset(self, pk):
		return self.get_serializer().Meta.model.objects.filter(state=True).filter(id=pk).first()
	
	def patch(self, request, pk=None):
		if self.get_queryset(pk):
			product_serializer = self.serializer_class(self.get_queryset(pk))
			return Response(product_serializer.data, status=status.HTTP_200_OK)
		return Response(
				{'message': 'No existe un producto con estos datos'}, 
				status=status.HTTP_400_BAD_REQUEST)
	
	def put(self, request, pk=None):
		if self.get_queryset(pk):
			product_serializer = self.serializer_class(self.get_queryset(pk))
			if product_serializer.isvalid():
				product_serializer.save()
				return Response(product_serializer.data, status=status.HTTP_200_OK)
		return Response(product_serializer.errors, status=status.HTTP_400_BAD_REQUEST)
```

### DestroyAPIView
Esta vista permite sobrescribir los métodos delete , entre otros.
mas: [DestroyAPIView](https://www.cdrf.co/3.13/rest_framework.generics/DestroyAPIView.html) en www.cdrf.co
```python
from rest_framework import generics, status
from rest_framework.response import Response

from apps.base.api import GeneraListApiView
from apps.products.api.serializers.products_serializers import ProductSerializer
from apps.products.models import Product 

class ProductDestroyAPIView(generics.DestroyAPIView):
	serializer_class = ProductSerializer

	def get_queryset(self):
		return self.get_serializer().Meta.model.objects.filter(state=True)
	
	def delete(self, request, pk = None):
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