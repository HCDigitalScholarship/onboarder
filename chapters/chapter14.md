---
title: '14 Forms and form data (May 28 AM)'
description:
  ""
prev: /chapter13
next: /chapter15
type: chapter
id: 14
---

<exercise id="1" title="Forms">

[w3schools](https://www.w3schools.com/html/html_forms.asp)
[Django docs forms](https://docs.djangoproject.com/en/3.0/topics/forms/)

```html
<form>
  <label for="fname">First name:</label><br>
  <input type="text" id="fname" name="fname"><br>
  <label for="lname">Last name:</label><br>
  <input type="text" id="lname" name="lname">
</form>
```

</exercise>

<exercise id="2" title="GET form">

create venv

`conda create -n django python=3.7`

`conda activate django`

`pip install django`


`django-admin startproject former`

`cd former`

`python manage.py startapp former_app`

`cd former`

`nano settings.py`

`add 'former_app' to INSTALLED_APPS`

`nano  former/urls.py`

add `import former_app.views as views`
and `path('', views.index, name="home"),`
to former/urls.py

`nano former_app/views.py `
add
```python
def index(request):
    return render(request, "index.html",)
```

 `mkdir former_app/templates`

`nano former_app/templates/index.html`

```html
 <!DOCTYPE html>
<html>
<head>
<title>Former</title>
</head>
<body>

<h1>This shall be the former</h1>

</body>
</html>
```

then add the form to `index.html`

```html
<form method="get">
  <label for="fname">First name:</label><br>
  <input type="text" id="fname" name="fname" value="John"><br>
  <label for="lname">Last name:</label><br>
  <input type="text" id="lname" name="lname" value="Doe">
  <input type="submit" value="Submit">
</form>
```

*note the GET requests in the logs*

add to def index(request):
```python
if request.GET:
    context = {}
    first_name = request.GET.get('fname', None)
    last_name = request.GET.get('lname', None)
    context['message'] = f"Hello {first_name} {last_name}"
    return render(request, 'index.html', context)
else:
    return render(request, "index.html",)
```
add to index.html
```html
<script>
    {% if message%}
    alert('{{ message }}');
    {% endif %}
</script>
```

</exercise>

<exercise id="3" title="POST form">

change `index.html`
```html
<form method="post">
{% csrf_token%}
...
</form>
```

change `views.py`
change GET to POST

<hr>
<h2>GET vs. POST</h2>
<p>The following table compares the two HTTP methods: GET and POST.</p>
<div class="w3-responsive">
<table class="w3-table-all notranslate">
  <tr>
    <th style="width:30%">&nbsp;</th>
    <th style="width:35%">GET</th>
    <th>POST</th>
  </tr>
  <tr>
    <td>BACK button/Reload</td>
    <td>Harmless</td>
    <td>Data will be re-submitted (the browser should alert the user that the data are about to be re-submitted)</td>
  </tr>
  <tr>
    <td>Bookmarked</td>
    <td>Can be bookmarked</td>
    <td>Cannot be bookmarked</td>
  </tr>
  <tr>
    <td>Cached</td>
    <td>Can be cached</td>
    <td>Not cached</td>
  </tr>
  <tr>
    <td>Encoding type</td>
    <td>application/x-www-form-urlencoded</td>
    <td>application/x-www-form-urlencoded or multipart/form-data. Use multipart encoding for binary data</td>
  </tr>
  <tr>
    <td>History</td>
    <td>Parameters remain in browser history</td>
    <td>Parameters are not saved in browser history</td>
  </tr>
  <tr>
    <td>Restrictions on data length</td>
    <td>Yes, when sending data, the GET method adds the data to the URL; and the length of a URL is limited (maximum URL length is 2048 characters)</td>
    <td>No restrictions</td>
  </tr>
  <tr>
    <td>Restrictions on data type</td>
    <td>Only ASCII characters allowed</td>
    <td>No restrictions. Binary data is also allowed</td>
  </tr>
  <tr>
    <td>Security</td>
    <td>GET is less secure compared to POST because data sent is part of the URL<br>
 <br>
 Never use GET when sending passwords or other sensitive information!</td>
    <td>POST is a little safer than GET because the parameters are not stored in browser history or in web server logs</td>
  </tr>
  <tr>
    <td>Visibility</td>
    <td>Data is visible to everyone in the URL</td>
    <td>Data is not displayed in the URL</td>
  </tr>
  </table>
</div>
<a href="https://www.w3schools.com/tags/ref_httpmethods.asp">src</a>
<hr>

</exercise>

<exercise id="4" title="Django forms">

`create a new file former_app/forms.py`

```python
from django import forms

class NameForm(forms.Form):
    first_name = forms.CharField(label='first_name', max_length=100)
    last_name = forms.CharField(label='last_name', max_length=100)
```

now edit `views.py`

```python
from former_app.forms import NameForm

def index(request):
    if request.POST:
        form = NameForm(request.POST)
        if form.is_valid():
          context = {}
          context['form'] = form
          first_name = form.cleaned_data['first_name']
          last_name = form.cleaned_data['last_name']
          context['message'] = f"Hello {first_name} {last_name}"
          return render(request, 'index.html', context)
    else:
        form = NameForm()
        return render(request, "index.html", {"form": form})
```
now edit `index.html`

```html
<form method="post">
{% csrf_token%}
  {{ form }}
  <input type="submit" value="Submit">
</form>
```
more on [Django forms](https://docs.djangoproject.com/en/3.0/topics/forms/)

</exercise>

<exercise id="5" title="Final Project">

<img src="https://target.scene7.com/is/image/Target/GUEST_4c383d0d-52f3-4190-adad-00dd21163e7f?wid=488&hei=488&fmt=pjpeg">

- Mad Libs is a game where you fill in missing words.  The player is asked to name an "adjective" or "verb."  The response is placed in the text to create funny stories.   
- Use the marked-up text below

```html
<p>A vacation is when you take a trip to some <span id="1" class="adjective"></span> place
with your <span id="2" class="adjective"></span> family. Usually you go to some place
that is near a/an <span id="3" class="noun"></span> or up on a/an <span id="4" class="noun"></span>.
A good vacation place is one where you can rclasse <span id="5" class="plural_noun"></span>
or play <span id="6" class="game"></span> or go hunting for <span id="7" class="plural_noun"></span>. I like
to spend my time <span id="8" class="ing_verb"></span> or <span id="9" class="ing_verb"></span>.
When parents go on a vacation, they spend their time eating
three <span id="10" class="plural_noun"></span> a day, and fathers play golf, and mothers
sit around <span id="11" class="ing_verb"></span>. Last summer, my little brother
fell in a/an <span id="12" class="noun"></span> and got poison <span id="13" class="plant"></span> all
over his<span id="14" class="body_part"></span>. My family is going to go to (the)
<span id="15" class="place"></span>, and I will practice <span id="16" class="ing_verb"></span>. Parents
need vacations more than kids because parents are always very
<span id="17" class="adjective"></span> and because they have to work <span id="18" class="number"></span>
hours every day all year making enough <span id="19" class="plural_noun"></span> to pay
for the vacation.</p>
``` 
[src](http://www.madlibs.com/content/uploads/2016/04/VacationFun_ML_2009_pg15.pdf)

- Using Beautifulsoup, Javascript, jQuery or pure Python, extract the id values from the spans to create a list of values.
For example `spans = ["adjective","adjective","noun"...]` or `spans = {"1":"adjective", "2":"adjective", "3":"noun"}`

- create a form with a field for each span with a label for the part of speech  
*hint* [field label](https://www.w3schools.com/tags/tag_label.asp)
- serve the form to a template 
- fill the spans in the text with the user's form responses. 
- return the completed mad lib to the user 

You can form teams or work on this alone. Ask for help at any time. You have until next Monday to complete the app. We will then look at all the entries and vote on our favorite as a group. 

</exercise>