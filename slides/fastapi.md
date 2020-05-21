---
type: slides

---

## GET request 

```python
from datetime import datetime
from fastapi import FastAPI, WebSocket

app = FastAPI()

@app.get("/")
def root():
    return { "time": datetime.now() }
```

--- 

# GET with path argument

```python
@app.get("/name/{name}")
async def name(name: str):
    return { "name" : name }
```

---

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

---

# GET with query

for example:

https://www.people.co/<span style="background-color: black; color: white;">?first_name=Andy</span>

````python
from fastapi import Request

@app.get("/people")
async def name(name: str, request: Request):
    first_name = request.query_param['first_name']  # in django: request.GET.get('first_name', None)
    person = [person for person in people if person['name'] == first_name]
    return person
```

--- 

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

---