
#### global urls.py:
```python
#Custom titles for admin
admin.site.site_header = 'Title'
admin.site.index_title = 'Subtitle'
admin.site.site_title = 'Window Title'

STATICFILES_DIRS = [
	os.path.join(BASE_DIR, 'static'),
]

```

#### Put a logo: settings.py
```python
TEMPLATES = [
	{
		'BACKENDS': '......',
		'DIRS': [os.path.join(BASE_DIR, 'templates/')]
	}
]
```

#### Custom project colors: in the file Django installed on our lib packages:
>env >Lib>site-packages>django>contrib>admin>templates>admin
Edit the file base_site.html

#### Change the css styles:
##### base_site.html
```Django
{% block extrastyle %}
	<style>
		#header {
			background-color: 'red'
		}
	</style>
{% endblock %}
```