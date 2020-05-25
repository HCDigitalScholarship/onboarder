---
title: '10 templates and dynamic web applications (May 26 AM)'
description:
  ""
prev: /chapter9
next: /chapter11
type: chapter
id: 10
---

<exercise id="1" title="Templates">

- Templates allow us to create reusable blocks of HTML.
We can re-use components like the navbar or footer.  Changes made to the block are reflected in all pages that rely on that block.
- Templates also let us pass data from the server and parse that data into valid HTML.  For example, the following sends a list of fish to the template, then creates an ordered list of fish. 

*views.py*
```python 
def my_view(request):
  context = {}
  context['fishes'] = ['one fish', 'two fish','three fish', 'blue fish',]
  return render('fishes.html', context)
```

*fishes.html*
```html
<ol>
{% for fish in fishes %}
  <li>{{ fish }}</li>
{% endfor %}
</ol>
```
</exercise>

<exercise id="2" title="Reading">

[Real Python Primer on Jinja Templating](https://realpython.com/primer-on-jinja-templating/)

[The Django template language](https://docs.djangoproject.com/en/3.0/ref/templates/language/)

</exercise>

<exercise id="3" title="Debates in Modern Web Development">
 
[Second-guessing the modern web](https://macwright.org/2020/05/10/spa-fatigue.html) 

["Advantages and Disadvantages of Django"](http://www.mindfiresolutions.com/blog/2018/04/advantages-and-disadvantages-of-django/)

[Design for Diversity: The Case of Ed / Alex Gil](https://des4div.library.northeastern.edu/design-for-diversity-the-case-of-ed-alex-gil/)

[Modern Web Development on the Jamstack New Techniques for Ultra Fast Sites and Web Applications by Mathias Biilmann & Phil Hawksworth](https://www.netlify.com/oreilly-jamstack/#download)

</exercise>