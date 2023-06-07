## Serializar modelos

- Serializador desde un modelo
	```python
	from rest_framework import serializers
	
	from apps.products.models import Product
	
	class ProductSerializer(serializers.ModelSerializer):
	
	    class Meta:
	        model = Product
	        exclude = ('state', 'created_date', 'modified_date', 'deleted_date')
	```

-   Personalizar cuando se tienen claves foráneas: Esta forma muestra toda la info en el JSON    
    ```python
    from rest_framework import serializers
    
    from apps.products.models import Product
    
    class ProductSerializer(serializers.ModelSerializer):
    	nombre_campo_llave = Serializador()
    
        class Meta:
            model = Product
            exclude = ('state', 'created_date', 'modified_date', 'deleted_date')
    ```

-   Personalizar cuando se tienen claves foráneas: Esta forma muestra el nombre de str    
    ```python
    from rest_framework import serializers
    
    from apps.products.models import Product
    
    class ProductSerializer(serializers.ModelSerializer):
    	nombre_campo_llave = serializers.StringRelatedField()
    
        class Meta:
            model = Product
            exclude = ('state', 'created_date', 'modified_date', 'deleted_date')
    ```

-   Personalizar sobrescribiendo el método to_representation()    
    ```python
    from rest_framework import serializers
    
    from apps.products.models import Product
    
    class ProductSerializer(serializers.ModelSerializer):
    
        class Meta:
            model = Product
            exclude = ('state', 'created_date', 'modified_date', 'deleted_date')
    
    		def to_representation(self, instance):
    			return {
    				'id': instance.id,
    				'description': instance.description,
    				'image': instance.image if instance.image != '' else '',
    				'campo_foraneo1': instance.campo_foraneo1.description,
    				'campo_foraneo2': instance.campo_foraneo2.description,			
    			}
    ```

## Serializar sin modelos
```python
from rest_framework import serializers

class ProductSerializer(serializers.Serializer):

	name = serializers.CharField(max_length=10)
```
