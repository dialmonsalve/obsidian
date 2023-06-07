
##### Based on classes - **Overwriting the dispatch** method
```python
from djang.views.generic import CreateView
from .models import Model
from .forms import InstanceForm 
from django.urls import reverse_lazy
from django.shortcuts import redirect

class CreateInstance(CreateView):
	model = Model
	template_name = 'instance/create.html'
	form_class = InstanceForm
	success_url = reverse_lazy('list_instance')

	def dispatch(self, request, *args, **kwargs):
		if not request.user.is_staff():
			return redirect(reverse_lazy('admin:login.html'))
		return super(CreateInstance, self).dispatch(request, *args, **kwargs)
```

#### Based on classes - **Overwriting the get** method
```python
from djang.views.generic import CreateView
from .models import Model
from .forms import InstanceForm 
from django.urls import reverse_lazy
from django.shortcuts import redirect

class CreateInstance(CreateView):
	model = Model
	template_name = 'instance/create.html'
	form_class = InstanceForm
	success_url = reverse_lazy('list_instance')

	def get(self, request, *args, **kwargs):
		if not request.user.is_autehenticated:
			return render(self.template_name)
		return redirect('login')
```

#### Based on classes - **Create a Mixing**
```python
from djang.views.generic import CreateView
from .models import Model
from .forms import InstanceForm 
from django.urls import reverse_lazy

class StaffRequireMixin(object):
	def dispatch(self, request, *args, **kwargs):
		if not request.user.is_staff():
			return redirect(reverse_lazy('admin:login.html'))
		return super(StaffRequireMixin, self).dispatch(request, *args, **kwargs)
	

'''
	Inherit from the StaffRequireMixin class to be used in classes that 
	require this validation. It must go first in the inheritance hierarchy 
	in order for it to apply the if-staff logic first.
'''
class CreateInstance(StaffRequireMixin, CreateView):
	model = Model
	template_name = 'instance/crear.html'
	form_class = InstanceForm
	success_url = reverse_lazy('listar_instance')
```

#### Based on classes - **using decorators**
```python
from django.views.generic import CreateView
from django.urls import reverse_lazy
from django.contrib.admin.views.decorator import staff_member_required
from django.utils.decorator import method_decorator
from .models import Model
from .forms import InstanceForm 

'''
	The second argument indicates which method should be decorated (in this
	case, the dispatch method). There are 2 more methods called 
	login_required and permission_required
'''

@method_decorator(staff_member_required, name='dispatch')
class CreateInstance(CreateView):
	model = Model
	template_name = 'instance/create.html'
	form_class = InstanceForm
	success_url = reverse_lazy('list_instance')
```

#### *Configure* the urls file

```python
from django.urls import path
from django.contrib.auth.decorators import login_required
from .views import (
	PageListView, 
	PageDetailView, 
	PageCreate, 
	PageUpdate, 
	PageDelete
)

pages_patterns = ([
	path('', login_required(PageListView.as_view()), name='pages'),
	path('<int:pk>/<slug:slug>/', login_required(PageDetailView.as_view()), name='page'),
	path('create/', login_required(PageCreate.as_view(), name='create')),
	path('update/<int:pk>/', login_required(PageUpdate.as_view()), name='update'),
	path('delete/<int:pk>/', login_required(PageDelete.as_view()), name='delete'),
], 'pages')
```
