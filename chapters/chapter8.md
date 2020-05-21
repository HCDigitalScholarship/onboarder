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

<exercise id="4" title="Booktweets">

## Challenge, create an app that checks every hour for new tweets containing the keyword "book"

**main.py**
```python
import twint

from datetime import datetime
from fastapi import FastAPI
from fastapi.responses import HTMLResponse
from fastapi import FastAPI, WebSocket

app = FastAPI()

@app.get("/")
async def get():
  #TODO use twint to get all tweets from the last hour that contain "book"
  tweets = {}
  return tweets

```

</exercise>
