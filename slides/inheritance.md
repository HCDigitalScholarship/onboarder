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

- When we render index.html, the template engine gets the code in base.html and places the contents of `{% block content %}` in the placeholder area. 

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

It is also common to see extra_css and extra_js blocks. These let you add js and css that are specific to a particular page. 

*base.html*
```html
<!doctype html>
<html>
  <head>
    {% include 'header.html' %}
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

{% block extra_css %}
<link rel="stylesheet" href="styles.css">
{% endblock %}

    {% block content %}
    <h1>This is my_page.html</h1>
    {% endblock %}

{% block extra_js %}
<script>
function my(event) {
    console.log(event);
}; 
</script>
{% endblock %}
```

---

Other common tags are 

- `{% load static %}` which is needed in Django to load static files.  They can then be added as such:
`<img src={% static 'my_image.png' %}>`  

- `{% load l10n %}` will be at the top of all multi-lingual pages using Django's localization features.  You'll also see the `trans` tag. For example,
`<h1>{% trans "this is the worst page" %}</h1>`.  

For more see [the Django docs](https://docs.djangoproject.com/en/3.0/topics/i18n/)

---

