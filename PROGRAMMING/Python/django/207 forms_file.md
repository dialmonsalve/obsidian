There are two ways to create forms
Create a forms file inside the app folder to which it belongs

##### **1. Generic forms** When is created by generic form, the view will be FormView
```python
from django import forms

class ContactForm(form.Form):
	name = forms.CharField(label="Name", required=True)
	email= forms.EmailField(label="Email", required=True)
	content = forms.CharField(
		label="Name", 
		required=True, 
		widget=forms.Textarea, 
		attr={ 'class': 'my-5', 'rows':3}
)
```
 
##### **2.  Base on a model**
```python
from django import forms
from .models import Model

class ContactForm(form.ModelForm):
	class Meta:
		model = Model	
		fields = ['title', 'content', 'order']
		labels = {
			'title' : 'Title', 
			'content' : 'Content', 
			'order': 'order',
	}
		widgets = {
	   "title": forms.TextInput(
					attrs={"class": "form-control", 'placeholder': 'Titulo'}
				),
		"content": forms.Textarea(attrs={"class": "form-control"}),
		"order": forms.NumberInput(attrs={"class": "form-control"}),
	}

	def clean_property(self):
		content = self.cleaned_data['content']
		if content < 10:
			raise forms.ValidationError(f'{content} must have more than 10 characters')
		return content
``` 