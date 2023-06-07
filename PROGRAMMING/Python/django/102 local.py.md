
```python

from .base import *

# SECURITY WARNING: don't run with debug turned on in production!
DEBUG = True  

ALLOWED_HOSTS = []

# Database

# https://docs.djangoproject.com/en/4.2/ref/settings/#databases  

DATABASES ={
	'default': {	
		'ENGINE' : get_secret('ENGINE'),		
		'NAME' : get_secret('DB_NAME'),		
		'USER' : get_secret('USER'),		
		'PASSWORD': get_secret('PASSWORD'),		
		'HOST' : get_secret('HOST'),		
		'PORT' : get_secret('PORT'),	
	}
}

# Static files (CSS, JavaScript, Images)
# https://docs.djangoproject.com/en/4.2/howto/static-files/
STATIC_URL = '/static/'
STATICFILES_DIR = ['static']  

MEDIA_URL = '/media/'
MEDIA_ROOT = 'media'
```