# Custom validation for models in Django admin

In Django Admin, you can add custom validations to your models by defining clean methods. 
There are two main ways to add custom validations in a Django model:

### 1. **Model-level Validation**

Model-level validation is useful for validating the entire model. You can define a `clean()` method in your model to add custom validation logic.

```python
from django.core.exceptions import ValidationError
from django.db import models

class MyModel(models.Model):
    name = models.CharField(max_length=100)
    age = models.IntegerField()

    def clean(self):
        # Custom validation logic
        if self.age < 18:
            raise ValidationError('Age must be at least 18.')

        # Call the parent class's clean method if needed
        super().clean()
```

### 2. **Field-level Validation**

For validating individual fields, you can use the `clean_<fieldname>()` method for each field that requires custom validation.

```python
from django.core.exceptions import ValidationError
from django.db import models

class MyModel(models.Model):
    name = models.CharField(max_length=100)
    age = models.IntegerField()

    def clean_age(self):
        if self.age < 18:
            raise ValidationError('Age must be at least 18.')
```

### 3. **Custom Validation in Django Admin**

If you want to apply custom validation logic specifically within the Django Admin, you can override the `save_model()` method in your `ModelAdmin` class to include validation.

```python
from django.contrib import admin
from django.core.exceptions import ValidationError

class MyModelAdmin(admin.ModelAdmin):
    def save_model(self, request, obj, form, change):
        try:
            obj.full_clean()  # This will call the model's clean() method
        except ValidationError as e:
            form.add_error(None, e)  # Add the error to the form
            return
        super().save_model(request, obj, form, change)

admin.site.register(MyModel, MyModelAdmin)
```

### Summary

- **Model-level validation**: Implement the `clean()` method in your model to validate the entire model.
- **Field-level validation**: Implement `clean_<fieldname>()` methods to validate individual fields.
- **Admin-specific validation**: Override the `save_model()` method in your `ModelAdmin` class to enforce model validations in the Django Admin.
  
