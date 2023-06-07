
#### **List objects**
```python
Instance.objects.all()
SELECT * FROM instance

Instance.objects.filter(field1='field')
SELECT * FROM instance WHERE field1='field'

Instance.objects.filter(field1='field', id=1)
SELECT * FROM instance WHERE campo1 like 'field' and id==1

Instance.objects.get(id=1)
```

#### **Create objects**
```python
Instance.objects.create(field1='field', field2='field',...)

nuevo = Instance(field1='field', field2='field',...) 
nuevo.save()

INSERT INTO instance(field1, field2,...) values ('field','field'...)
```

#### **Create objects with multiple fields**
```python
class User(models.Model):

	def form_valid(self, form):

		loans = []

		for books in form.cleaned_data['books']:
			loan = Loan(
				reader=form.cleaned_data['reader'],
				book=book,
				loan_date=date.today(),
				is_comeback=False
			)
			loans.append(loan)

		Loans.objects.bulk_create( # bulk_update
			loans
		)
```

#### **Update objects**
```python
Instance.objects.get(id=1).filter()
```

#### **Relationship**
```python
OneToOneField 1:1
ForeignKey 1:N
ManyToManyField N:M
``` 
