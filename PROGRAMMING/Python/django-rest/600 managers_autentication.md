## Authentication with token:
```python

	class ListProductUser(ListApiView):
		serializer_class = ProductSerializer
		authentication_classes = (TokenAuthentication,)
		permission_classes = [isAuthenticated]

		def get_queryset(self):
			user = self.request.user
			return Product.objects.function_manager(user)
	
```

#### Permissiones
Allows edit our own profile
```python
from rest_framework import permisions

class UpdateOwnProfile(permissions.BasePermission):

	def has_object_permission(self, request, view, obj):
		if request.method in permissions.SAFE_METHODS:
			return True
		return obj.id == request.user.id
	
```
