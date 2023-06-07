### api.py: Se definen las funciones
```python
from rest_framework import status
from rest_framework.response import Response
from rest_framework.views import APIView
from apps.users.api.serializers import UserSerializer, UserListSerializer
from apps.users.models import User

from rest_framework.decorators import api_view 

@api_view(['GET', 'POST'])
def user_api_view(request):
	if request.method == 'GET':
		users = User.objects.all().values('id', 'username', 'email', 'password')
		users_serializer = UserListSerializer(users, many = True)
		return Response(users_serializer.data, status=status.HTTP_200_OK)

	elif request.method == 'POST':
		user_serializer = UserSerializer(data=request.data)
		if user_serializer.is_valid():
			user_serializer.save()
			return Response(user_serializer.data, status=status.HTTP_201_CREATE
		return Response(user_serializer.errors , status=status.HTTP_400_BAD_REQUEST)
	

@api_view(['GET', 'PUT', 'DELETE'])
def user_detail_api_view(request, pk=None):
	
	user = User.objects.filter(id=pk).first()
	if user: 
		if request.method == 'GET':
			user_serializer = UserSerializer(user)
			return Response(user_serializer.data, status=status.HTTP_200_OK)
		
		elif request.method == 'PUT':

			user_serializer = UserSerializer(user, data=request.data)
			if user_serializer.is_valid():
				user_serializer.save()
				return Response(user_serializer.data, status=status.HTTP_200_OK)
			return Response(user_serializer.errors, status=status.HTTP_400_BAD_REQUEST)
		
		elif request.method == 'DELETE':  
			user.delete()
			return Response({'message': 'Usuario eliminado correctamente'}, status=status.HTTP_200_OK)
	return Response({'message': 'No se ha encontrado usuario con estos datos'}, status=status.HTTP_400_BAD_REQUEST)
```

### serializers.py - Serializando con un modelo 
```python
from rest_framework import serializers
from apps.users.models import User

class UserSerializer(serializers.ModelSerializer):
	class Meta:
		model = User
		fields = '__all__'
		# fields = ['name', 'lastname'] #? Muestra campos que se quieran

	def create(self, validated_data):
		user = User(**validated_data)
		user.set_password(validated_data['password'])
		user.save()
		return user

	def update(self, instance, validated_data):
		updated_user = super().update(instance, validated_data)
		updated_user.set_password(validated_data['password'])
		updated_user.save()
		return updated_user

class UserListSerializer(serializers.ModelSerializer):
	class Meta:
		model = User

	def to_representation(self, instance):
		return {
			'id': instance['id'],
			'username': instance['username'],
			'email': instance['email'],
			'password': instance['password'],
		}
```

### serializers.py - Serializando sin modelo
```python
class TestUserSerializer(serializers.Serializer):
	
	#* Se definen los campos que tendrá el serializador genérico
	name = serializers.CharField(max_length = 200)
	email = serializers.EmailField()
	
	#? De manera opcional, se pueden personalizar los validadores con los métodos definiendolos así:
	#? def validate_nombre_campo(self, value). Las validaciones se ejecutan tanto para crear como para actualizar
	def validate_name(self, value):
		return value
	
	def validate_email(self, value):
		
		#! Para hacer una válidación personal con los campos de la propia clase, antes de ser validado se pasa como argumento al validador el diccionario de contexto
		
		if self.validate_name(self.context['name']) in value:
			raise serializers.ValidationError('El email no puede contener el nombre')
		
		return value
	
	def validate(self, data):
		return data
	
	#! Para crear el serializador, se usa el método create y antes se debe pasar el método save()
	def create(self, validated_data):
		return self.model.objects.create(**validated_data)
	
	def update(self, instance, validated_data):
		instance.name = validated_data.get('name', instance.name)
		instance.email = validated_data.get('email', instance.email)
		instance.save()
		return instance
	
	#! El método save(), se puede reescribir cuando no queramos hacer inserciones en la db
	def save(self):
		print(self)
```

### urls.py
```python
from django.urls import path
from apps.users.api.api import UserApiView, user_api_view, user_detail_api_view

urlpatterns = [
	path('usuario/', user_api_view, name='usuario_api'),
	path('usuario/<int:pk>/', user_detail_api_view, name='usuario_detail_api_view'),
]
```