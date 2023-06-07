1.  Instalar: pip install drf-yasg

-   2.  urls.py global
    ```python
    from rest_framework import permissions
    
    from drf_yasg.views import get_schema_view
    from drf_yasg import openapi
    
    schema_view = get_schema_view(
        openapi.Info(
            title='',
            default_version='',
            description='',
            terms_of_service='',
            contact=openapi.Contact(email=''),
            license=openapi.License(name=''),
        ),
        public=True,
        permission_classes=(permissions.AllowAny),
    )
    
    urlpatterns = [
        re_path(r'^swagger(?P<format>\\.json|\\.yaml)$', schema_view.without_ui(cache_timeout=0), name='schema-json'),
        path(r'swagger/', schema_view.with_ui('swagger', cache_timeout=0), name='schema-swagger-ui'),
        path(r'redoc/', schema_view.with_ui('redoc', cache_timeout=0), name='schema-redoc'),
    ]
    ```

-   3.  Instalar app
    ```python
    THIRD_APPS = [
        'rest_framework',
        'simple_history',
        'drf_yasg'
    ]
    ```