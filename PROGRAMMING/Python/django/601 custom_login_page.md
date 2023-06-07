
### Login
```python
from django.views.generic.edit import FormView

class LoginUser(FormView):

	template_name = 'users/login.html'		
	form_class = LoginForm		
	success_url = reverse_lazy('home_app:panel')

	def form_valid(self, form):	
	
		user = authenticate(		
			username=form.cleaned_data['username'],			
			password=form.cleaned_data['password'],		
		)
	
		login(self.request, user)
	
		return super(LoginUser, self).form_valid(form)
```

### Logout
```python
class LogOutView(View):

	def get(self, request, *args, **kwargs):
	
		logout(request)			
		return HttpResponseRedirect(			
		reverse('users_app:user-login')

		)
```

### Change password
```python
class UpdatePasswordView(LoginRequiredMixin, FormView):

	template_name = 'users/update.html'		
	form_class = UpdatePasswordForm # Create Form		
	success_url = reverse_lazy('users_app:user-login')		
	login_url = reverse_lazy('users_app:user-login')

def form_valid(self, form):	
	user_authenticated = self.request.user 
	user = authenticate(		
	username=user_authenticated.username,		
	password=form.cleaned_data['password1'],		
	)
	
	if user:		
		new_password = form.cleaned_data['password2']			
		user_authenticated.set_password(new_password)			
		user_authenticated.save()
	logout(self.request)
	
	return super(UpdatePasswordView, self).form_valid(form)
```