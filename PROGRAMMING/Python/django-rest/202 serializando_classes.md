### serializers.py
```python
from rest_framework import serializers

from apps.products.models import Product

class ProductSerializer(serializers.ModelSerializer):
	measure_unit = serializers.PrimaryKeyRelatedField(queryset=MeasureUnit.objects.filter(state = True))
	category = serializers.PrimaryKeyRelatedField(queryset=CategoyProduct.objects.filter(state = True))

	class Meta:
		model = Product
		exclude = ('state', 'created_date', 'modified_date', 'deleted_date')
		extra_kwargs = {
			'password': {
				'write_only': True,
				'style': {'input_type':'password'}
			}
		}
		
	def to_representation(self, instance):
		return {
			'id': instance.id,
			'name': instance.name,
			'description': instance.description,
			'image': instance.image if instance.image != '' else '',
			'measure_unit': instance.measure_unit.description if instance.measure_unit is not None else '',
			'category': instance.category.description if instance.category is not None else '',			
		}
```

### views.py
Se pueden implementar las vistas [[103 genericApiViews|genéricas]] o las vistas [[102 viewSets|viewsets]]
### urls.py
```python
from django.urls import path
from apps.products.api.views.general_views import (
	CategoyProductListApiView, 
	IndicatorListApiView,
	MeasureUnitListApiView, 
)
from apps.products.api.views.product_views import (
	ProductCreateAPIView,
	ProductListAPIView,
	ProductRetrieveAPIView,
	ProductDestroyAPIView,
	ProductUpdateAPIView
)

urlpatterns = [
	path('measure_unit/', MeasureUnitListApiView.as_view(), name='measure_unit'),
	path('category_product/', CategoyProductListApiView.as_view(), name='category_product'),
	path('indicator/', IndicatorListApiView.as_view(), name='indicator'),
	path('product/', ProductListAPIView.as_view(), name='product'),
	path('product/create/', ProductCreateAPIView.as_view(), name='create_product'),
	path('product/retrieve/<int:pk>/', ProductRetrieveAPIView.as_view(), name='retrieve_product'),
	path('product/destroy/<int:pk>/', ProductDestroyAPIView.as_view(), name='destroy_product'),
	path('product/update/<int:pk>/', ProductUpdateAPIView.as_view(), name='update_product'),
]
```