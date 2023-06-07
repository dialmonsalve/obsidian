
#### Based on functions

- This file shows how the configuration of the urls file should be based on functions
	```python
	from django.urls import path 
	from . import views 
	
	urlpatterns = [ 
		path('', views.home, name='home'), 
		path('about/', views.about, name='about'), 
		path('contact/', views.contact, name='contact'), 
		path('<int:page_id>/<slug:page_slug>/', views.page, name='page'), 
	]
	```
-   Configuration to urls-global
    ```python
    from django.urls import path, include
    
    urlpatterns = [ 
    	path('ruta/', include('app.urls')),
    ]
    ```

#### Based on classes

- This file shows how the configuration of the urls file should be based on classes
	```python
	from django.urls import path 
	from .views import (
		PageListView, 
		PageDetailView, 
		PageCreate, 
		PageUpdate, 
		PageDelete )

	pages_patterns = ([ 
		path('', PageListView.as_view(), name='pages'),
		path('<int:pk>/<slug:slug>/', PageDetailView.as_view(), name='page'),
		path('create/', PageCreate.as_view(), name='create'),
		path('update/<int:pk>/', PageUpdate.as_view(), name='update'),
		path('delete/<int:pk>/', PageDelete.as_view(), name='delete'), 
	], 'pages')
	```

-   Configuration to urls-global
    ```python
    from django.contrib import admin 
    from django.urls import path, include 
    from pages.urls import pages_patterns 
    
    urlpatterns = [ 
	    path('pages/', include(pages_patterns)),
		path('admin/', admin.site.urls),
	]
    ```
