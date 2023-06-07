- #### serializers.py
    ```python
    class VentaReporteSerializer(serializers.ModelSerializer):
    
        productos = serializers.SerializerMethodField()
    
        class Meta:
            model = Sale
            fields = ('__all__', 'productos')
    
        
        def get_products(self, obj):
            query = SaleDetail.objects.products_by_sale(obj.id)
    
            product_serialized = DetailSaleProductSerializer(query, many=True).data
    
            return product_serialized
    
    class DetailSaleProductSerializer(serializers.ModelSerializer):
    	model = SaleDetail
    	fields = ('__all__')
    ```

- #### managers.py
    ```python
    from django.db import models
    
    class SaleDetailManager(models.Manager):
    
        def products_by_sale(self, venta_id):
            consulta = self.filter(
                sale__id=venta_id
            ).order_by('count', 'product__name')
            return consulta
    ```