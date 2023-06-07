### Basadas en funciones
#### urls.py
```python
from django.urls import path
from apps.users.api.api import UserApiView, user_api_view, user_detail_api_view

urlpatterns = [
	path('usuario/', user_api_view, name='usuario_api'),
	path('usuario/<int:pk>/', user_detail_api_view,name='usuario_detail_api_view'),
]
```

### Basadas en viewsets
#### routers.py
```python
from rest_framework.routers import DefaultRouter
from apps.products.api.views.product_viewsets import ProductViewSet

router = DefaultRouter()

router.register(r'products', ProductViewSet, basename='products')

urlpatterns = router.urls
```

### Basadas en genericViews
#### urls.py
```python
from django.urls import path
from apps.users.api.api import UserApiView, user_api_view, user_detail_api_view

urlpatterns = [
	path('usuario/', user_api_view, name='usuario_api'),
	path('usuario/<int:pk>/', user_detail_api_view,name='usuario_detail_api_view'),
]
```