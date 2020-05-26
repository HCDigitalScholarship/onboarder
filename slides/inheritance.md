---
type: slides

---

Template inheritance allows us to create a consistent look across a site.  We create a navbar block, for example, that is used in all of the site's pages.  Any changes made in the navbar file will appear in any page using that block.  This saves us from having to make updates in every single page. 

<img width="30%" src="https://i.pinimg.com/originals/96/e3/7e/96e37e7c18b31277d248aa5dda182fa8.jpg" />

---

In most of our projects, there is a `templates` directory as well as a `base.html` file. The base file isn't the index, but sets the layout for all of the site. Blocks have an opening `{% block <name> %}` and `{% endblock %}`

*base.html*
```html
<!doctype html>
<html>
  <body>
    {% block content %}{% endblock %}
  </body>
</html>
```

- note the placeholder for `{% block content %}`

---

Our index file is actually a content block:

*index.html*
```html
{% extends "base.html" %}
{% block content %}
<h1>This is the index page!</h1>
{% endblock %}
```

- When we render index.html, the template engine gets the code in `base.html` and places the contents of `{% block content %}` from `index.html` in the placeholder area. 

---

Here is a common use of template inheritance.  We load the code from `header.html` and `footer.html` and place it in the head and footer sections of the page. 

```html
<!doctype html>
<html>
  <head>
    {% include 'header.html' %}
  </head>

  <body>
    {% block content %}{% endblock %}
  </body>

  <footer>
    {% include 'footer.html' %}
  </footer>
</html>
```

---

It is also common to see `extra_css` and `extra_js` blocks. These let you add js and css that are specific to a particular page.  You can also create a unique title (the text in the browser tab) for each page.  

*base.html*
```html
<!doctype html>
<html>
  <head>
    {% include 'header.html' %}
    <title>{% block title %}{% endblock %}</title>
    {% block extra_css %}{% endblock %}
  </head>

  <body>
    {% block content %}{% endblock %}
    {% block extra_js %}{% endblock %}
  </body>

  <footer>
    {% include 'footer.html' %}
  </footer>
</html>
```

---

*my_page.html*

```html
{% extends "base.html" %}

{% block title %}My Own Title{% endblock %}
{% block extra_css %}
<link rel="stylesheet" href="this_page_has_style.css">
{% endblock %}

    {% block content %}
    <h1 onclick="my_function(this);">This is my_page!</h1>
    {% endblock %}

{% block extra_js %}
<script>
function my_function(event) {
    console.log(event);
}; 
</script>
{% endblock %}
```

---

# Conditions 
```html
{% if fishes %}
{{ fishes}}
{% else %}
<p>no fishes today</p>
{% endif %}
```

---

# urls 

In Django, you can point to any of your views by name.

*urls.py*
```python
from django.urls import include, path

urlpatterns = [
    path('/about', views.about, name="about'),
] 
```

*my_template.html*
`<a href="{% url 'about' %}">About</a>`  

--- 

# Other common tags are 

- `{% load static %}` which is needed in Django to load static files.  They can then be added as such:
`<img src="{% static 'my_image.png' %}" />`  

- `{% load l10n %}` will be at the top of all multi-lingual pages using Django's localization features.  You'll also see the `trans` tag. For example,
`<h1>{% trans "this is the worst page" %}</h1>`.  

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