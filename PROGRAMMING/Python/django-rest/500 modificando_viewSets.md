#### Método perfom_created : 
Permite adicionar valores por defecto a las llaves que no sean obligatorias en un modelo por ejemplo
-  viewset.py
	```python
	class ProductViewSet(viewsets.ModelViewSet):
		serializer_class = ProductSerializer
		queryset  = Product.objects.all()


		def perform_create(self, serializer):

		serializer.save(
			video="url"
		)

		return Response({'code':'ok'})
	```
