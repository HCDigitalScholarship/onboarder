---
type: slides

---

# other common tags 

a. ``{% load static %}`` which is needed in Django to load static files.  They can then be added as such:
``<img src="{% static 'my_image.png' %}" />``  

b. ``{% load l10n %}`` will be at the top of all multi-lingual pages using Django's localization features.  You'll also see the `trans` tag. For example,
``<h1>{% trans "this is the worst page" %}</h1>``.  

Django will create a file that translators can use with any string in the trans tag.  When the language is changed, Django will use the correct-language string for this string.  

For more see [the Django docs](https://docs.djangoproject.com/en/3.0/topics/i18n/)


---


In addition to iteration and conditions, you can 

- render html from the view [`{{ my_html|safe }}`](https://docs.djangoproject.com/en/3.0/ref/templates/builtins/#safe)
- add lorem ipsum filler text [`{% lorem %}`](https://docs.djangoproject.com/en/3.0/ref/templates/builtins/#lorem)
- turn string into slug (for urls), [`{{ value|slugify }}`](https://docs.djangoproject.com/en/3.0/ref/templates/builtins/#slugify)
- turn plain text with line breaks ('\n') into HTMl [`{{ value|linebreaks }}`](https://docs.djangoproject.com/en/3.0/ref/templates/builtins/#linebreaks) 

---

<img src="djangopony.png" />