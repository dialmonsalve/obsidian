## APIView : Vista genérica

^944dd4

Sobrescribiendo el método get y serializando un campo con una relación de muchos a muchos
```python

	class UserApiView(APIView):
		def get(self, request):
			users = User.objects.all()
			useres_serializer = UserSerializer(users, many = True)
			return Response(data=useres_serializer.data, status=status.HTTP_200_OK)

```

Sobrescribiendo los métodos get, post, put, patch y delete
```python
	from rest_framework import APIView, status
	from rest_framework.response import Response

	from . import serializers
	
	class HelloApiView(APIView):

		serializer_class = serializers.HelloSerializer
	
		# MÉTODO GET		
		def get(self, request, format=None):
			an_apiview = [
				'Metodos http usados como funciones(get, post, patch, put, delete)',
				'Es similar a una vista tradicional de Django',
				'Da mas control sobre las logica de las aplicaciones',
				'Es mapeado manualmente por las urls'
			]
			return Response({'message': 'hello', 'an_apiview': an_apiview})

		# MÉTODO POST
		def post(self, request):
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

		# MÉTODO PUT
		def put(self, request, pk=None):
			return Response({'method': 'PUT'})
			
		# MÉTODO PATCH
		def patch(self, request, pk=None):
			return Response({'method': 'PATCH'})
			
		# MÉTODO DELETE
		def delete(self, request, pk=None):
			return Response({'method': 'DELETE'})
```

APIView es la vista más genérica. A partir de esta heredan todas las vistas en django rest incluidas las [[102 viewSets|viewSets]] y las [[103 genericApiViews|genericViews]], entre otras. A continuación una representación gráfica de la herencia de algunas clases en django rest framework y su implementación

## [[101 apiViews#^944dd4|apiViews]]
  - ### [[103 genericApiViews#genericApiViews|GenericAPIView]]
    - #### [[103 genericApiViews#createApiView|CreateAPIView]]
    - #### [[103 genericApiViews#ListApiView|ListAPIView]]
    - #### [[103 genericApiViews#RetrieveAPIView|RetrieveAPIView]]
    - #### [[103 genericApiViews#UpdateAPIView|UpdateAPIView]]
    - #### [[103 genericApiViews#DestroyAPIView|DestroyAPIView]]
  - ### [[102 viewSets|ViewSet]]
    - #### ReadOnlyModelViewSet
      - ##### ReadOnlyViewSet
        - ######  ListModelMixin
        - ###### RetrieveModelMixin
      - ##### GenericReadOnlyViewSet
        - ###### ListModelMixin
        - ###### RetrieveModelMixin
    - #### [[102 viewSets#ModelViewSet|ModelViewSet]]
      - ##### ReadOnlyModelViewSet
        - ###### ReadOnlyViewSet
          - ListModelMixin
          - RetrieveModelMixin
      - ##### GenericViewSet
        - ###### CreateModelMixin
        - ###### RetrieveModelMixin
        - ######  UpdateModelMixin
        - ###### DestroyModelMixin