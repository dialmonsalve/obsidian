
Allows you to send signalso triggers before or after certain actions. For example, register a profile after it is created so as not to have users without information or null
```python
from django.contrib.auth.models import User
from django.db import models
from django.dispatch import receiver
from django.db.models.signals import post_save

class Profile(models.Model):
	user = models.OneToOneField(User, on_delete=models.CASCADE)
	campos adicionales

@receiver(post_save, sender=User)
def ensure_profie_exists(sender, instance,  **kgwargs):
	if kgwargs.get('created', False): 
		Profile.objects.get_or_create(user=instance)

# Another way to use
post_save.connect(ensure_profie_exists, sender=User)
```
