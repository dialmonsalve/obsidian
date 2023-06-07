- #### serializers.py    
    ```python
    class ArrayIntegerSerializer(serializer.ListField):
    	
    	child = serializer.IntegerField()
    
    class ProcesoVentaSerializer(serializers.Serializer):
    	type_invoice = serializer.ChardField()
    	.....
    	products = ArrayIntegerSerializer()
    	
    ```
    
- #### views.py
    ```python
    class ....(CreateApiView):
    	....
    	products = Product.objects.filter(
    		id__in=serializer.validated_data['productos']
    	)
    	
    	cantidades = serializer.validated_data['cantidades']
    
    	for producto, cantidad in zip(productos, cantidades):
    		venta_detalle = SaleDetail(
    			sale=venta,
    			product=producto,
    			count=cantidad,
    			price_purcharse=producto.price_purcharse,
    			price_sale=producto.price_sale
    		)
    		amount = amount + product.price_sale * cantidad
    		count = count+ cantidad
    		ventas_detalle.append(venta_detalle)
    	venta.amount = amount
    	venta.count = count
    	venta.save()
    
    	SaleDetail.objects.bulk_create(ventas_detalle)
    ```