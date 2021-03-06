# Forms vs ModelForms

Forms created from `forms.Form` are manually configured by you. You're better off using these for forms that do not directly interact with models. For example - a contact form, or a newsletter subscription form, where you might not necessarily be interacting with the database.

Where as a form created from `forms.ModelForm` will be automatically created and then can later be tweaked by you. The best examples really are from the superb documentation provided on the Django website.

## forms.Form:

**Documentation:** [Form objects](http://docs.djangoproject.com/en/dev/topics/forms/#form-objects)
Example of a normal form created with `forms.Form`:

```py
from django import forms

class ContactForm(forms.Form):
    subject = forms.CharField(max_length=100)
    message = forms.CharField()
    sender = forms.EmailField()
    cc_myself = forms.BooleanField(required=False)

```

## forms.ModelForm:

**Documentation:** [Creating forms from models](http://docs.djangoproject.com/en/dev/topics/forms/modelforms/#topics-forms-modelforms)

> **Straight from the docs:**
> If your form is going to be used to directly add or edit a Django model, you can use a `ModelForm` to avoid duplicating your model description.

Example of a model form created with `forms.Modelform`:

```py
from django.forms import ModelForm
from . import models

# Create the form class.
class ArticleForm(ModelForm):
    class Meta:
        model = models.Article
```

This form automatically has all the same field types as the Article model it was created from.
