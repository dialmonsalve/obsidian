
## Based on functions

#### This file shows how the configuration of the views file should be based on functions
```python
from django.shortcuts import render, redirect
from foms import InstanceForm

# Create your views here.
def home(request):
	return render(request, "core/home.html")

def about(request):
	return render(request, "core/about.html")

def contact(request):
	return render(request, "core/contact.html")

# POST method
def create_instance(request):
	if request.method == 'POST':
		instance_form = InstanceForm(request.POST) # Django Form
		if instance_form.is_valid():
			instance_form.save()
			return redirect('index') # Name of page
	else:
		instance_form = InstanceForm()
	return redirect(request, 'instance/create.html', {'instance_form ': instance_form })

# GET method
def list_instance(request):
	instance = Instance.objects.all()
	return render(request, 'instance/list.html', {'instance': instance })

#Eidit
def edit_instance(request, id):
	instance = Instance.objects.get(id=id)
	if request.method == 'GET':
		instance_form = InstanceForm(instance = Instance)
	else:
		instance_form = InstanceForm(request.POST, instance = Instance)
		if instance_form.isvalid():
			instance.save()
		return redirect('index')
	return render(request, 'instance/create.html', {'instance_form': instance_form })

# Delete completely
def delete_instance(request, id):
	instance = Instance.objects.get(id=id)
	if request.method == 'POST':
		instance.delete()
		return redirect ('instance:listar_instance')
	return render(request, 'instance/delete.html', {'instance': instance })

# Logic delete
def delete_instance(request, id):
	instance = Instance.objects.get(id=id)
	if request.method == 'POST':
		instance.estado = False
		instance.save()
		return redirect ('instance:list_instance')
	return render(request, 'instance/delete.html', {'instance': instance })
```

## Based on classes

#### This file shows how the configuration of the views file should be based on classes
```python
from django.shortcuts import get_object_or_404 
from django.views.generic.list import ListView 
from django.views.generic.detail import DetailView 
from registration.models import Profile

# Create your views here. 
class ProfileListView(ListView): 
	model = Profile template_name = 'profiles/profile_list.html' 
	paginate_by = 3

class ProfileDetailView(DetailView): 
	model = Profile 
	template_name = 'profiles/profile_detail.html' 
	succes_url = reverse_lazy('index') 
	
	def get_object(self): 
		return get_object_or_404(
			Profile, 
			user__username=self.kwargs['username']
		)
```

## kind of views
There are different types of views, this allows create template views pre-built
#### Generic views    
```python
from djang.views.generic import View

class Index(View):
	
	def get(self, request, *args, **kwargs):
		return render(request, 'index.html')
```

##### TemplateView    
```python
from djang.views.generic import TemplateView

class Index(TemplateView):	
	template_name = 'index.html'

```

#### ListView    
```python
from djang.views.generic import ListView
from .models import Model

class ListInstance(ListView):
	model = Model
	template_name = 'instance/list.html'
	context_object_name = 'lista' # Allows you to pass the variable and use it as an iterator, if you don't provide it you must iterate with the variable called objects
	queryset = Model.objects.filter(estado=True)    	
```

#### UpdateView    
```python
from djang.views.generic import UpdateView
from .models import Model
from .forms import InstanceForm 
from django.urls import reverse_lazy

class UpdateInstance(UpdateView):
	model = Model
	template_name = 'instance/crear.html'
	form_class = InstanceForm
	success_url = reverse_lazy('listar_instance')
```

#### CreateView    
```python
from djang.views.generic import CreateView
from .models import Model
from .forms import InstanceForm 
from django.urls import reverse_lazy

class CreateInstance(CreateView):
	model = Model
	template_name = 'instance/crear.html'
	form_class = InstanceForm
	success_url = reverse_lazy('listar_instance')
```

#### DeleteView    
```python
# Direct deleting
from djang.views.generic import DeleteView
from .models import Model
from .forms import InstanceForm 
from django.urls import reverse_lazy

class DeleteInstance(DeleteView):
	model = Model
	success_url = reverse_lazy('list_instance')

# Logical delete
class DeleteInstance(DeleteView):
	model = Model

	def post(self, request, pk, *args, **kwargs):
		object = Model.objects.get(id=pk)
		object.estado == False
		object.save()
		return redirect('list_instance')
```

#### formView    
```python 
from django.chortcuts import render
from django.views.generic.edit import FormView
from django.urls import reverse_lazy

from apps.app.models import Model
from .forms import NewForm

class NewInstanceView(FormView):
	template_name = 'path/name.html'
	form_class = NewForm
	success_url = reverse_lazy('list_instance')

def form_valid(self, form):
	name = form.cleaned_data['name']
	last_name = form.cleaned_data['last_name']
	Model.objects.create(
		first_name = name,
		lastname = last_name
	)
	return super(NewInstanceView, self).form_valid(form)
```