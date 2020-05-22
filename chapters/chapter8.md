---
title: '8 request / response (May 22 AM)'
description:
  "We begin working with FastAPI and the interaction between client-side and server-side"
prev: /chapter7
next: /chapter9
type: chapter
id: 8
---

<exercise id="1" title="FastAPI/Starlette">

1. [install FastAPI](https://fastapi.tiangolo.com/tutorial/#install-fastapi)
2. [Hello World](https://fastapi.tiangolo.com/tutorial/first-steps/#first-steps)
3. [Paths](https://fastapi.tiangolo.com/tutorial/path-params/#path-parameters)
4. [Response](https://fastapi.tiangolo.com/tutorial/response-model/)
5. [Docs](https://fastapi.tiangolo.com/tutorial/response-model/#see-it-in-the-docs)

</exercise>

<exercise id="2" title="request / response " type="slides">

<slides source="fastapi">
</slides>

</exercise>

<exercise id="3" title="Django">

1. https://docs.djangoproject.com/en/3.0/ref/request-response/
2. https://developer.mozilla.org/en-US/docs/Learn/Server-side/Django/Introduction

</exercise>


<exercise id="4" title="GET request">

## GET request 

```python
from datetime import datetime
from fastapi import FastAPI, WebSocket

app = FastAPI()

@app.get("/")
def root():
    return { "time": datetime.now() }
```
</exercise>

<exercise id="5" title="GET with path argument">

# GET with path argument

```python
@app.get("/name/{name}")
async def name(name: str):
    return { "name" : name }
```
</exercise>

<exercise id="6" title="use browser url to query data">

# use browser url to query data 

```python 
people = []
people.append({'name': "Andy", "address": "88 Featherbed Lane, Bryn Mawr, PA"})
people.append({'name': "Mike", "address": "23 Dupont Place, Wilmington, DE"})

@app.get("/people/{name}")
async def name(name: str):
    person = [person for person in people if person['name'] == name]
    return person
```

</exercise>

<exercise id="7" title="GET with query">


# GET with query

for example:

<p>https://www.people.co/<span style="background-color: blue; color: white;">?first_name=Andy</span></p>

```python
from fastapi import Request

@app.get("/people")
async def name(name: str, request: Request):
    first_name = request.query_param['first_name']  
    person = [person for person in people if person['name'] == first_name]
    return person
```

</exercise>

<exercise id="8" title="types of response">

# types of response

[available response types](https://fastapi.tiangolo.com/advanced/custom-response/#available-responses)

- HTMLResponse

```python
def generate_html_response():
    html_content = """
    <html>
        <head>
            <title>Some HTML in here</title>
        </head>
        <body>
            <h1>Look ma! HTML!</h1>
        </body>
    </html>
    """
    return HTMLResponse(content=html_content, status_code=200)
```

</exercise>

<exercise id="9" title="HTML Templates">


# HTML Templates

```python
from fastapi.templating import Jinja2Templates
from fastapi.staticfiles import StaticFiles

templates = Jinja2Templates(directory="templates")
app.mount("/assets", StaticFiles(directory=static_path), name="assets")

@app.get("/")
def home():
    context = {} # A dictionary with data that we pass to the template engine to render
    context['greeting'] = "Welcome to my page!"

    page = templates.TemplateResponse(
        "about.html", {"request": Request, "context": context}
    ).body
```

**index.html**
```html
 <html>
        <head>
            <title>The Title</title>
        </head>
        <body>
            <h1>{{ greeting }}</h1>
        </body>
    </html>
```

</exercise>

<exercise id="10" title="redirect">
 

# redirect (to another site or view)

```python
@app.get("/typer")
async def read_typer():
    return RedirectResponse("https://typer.tiangolo.com")

```

```python 
from django.shortcuts import redirect

def my_view(request):
    return redirect(some_other_view)
```
</exercise>

<exercise id="11" title="Booktweets">

## Create an app that checks every hour for new tweets containing the keyword "book"

**main.py**
```python
import twint

from datetime import datetime
now = datetime.now()

from fastapi import FastAPI
from fastapi.responses import HTMLResponse
from fastapi import FastAPI, WebSocket

app = FastAPI()

@app.get("/")
async def get():
  #TODO use twint to get all tweets from the last 24-hours that contain the word "book"
  tweets = twint.Config()
  tweets.Search = ...
  tweets.Since = ...
  tweets.Until = ...
  tweets.Pandas = True
  tweets.Hide_output = True
  df = twint.storage.panda.Tweets_df
  return df.to_json()

```

</exercise>
