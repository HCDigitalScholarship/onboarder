---
type: slides

---

---

## synchronous response 

```python
from datetime import datetime
from fastapi import FastAPI, WebSocket

app = FastAPI()

@app.get("/")
def root():
    return { "time": datetime.now() }
```

--- 

```python
@app.get("/name/{name}")
async def name(name: str):
    return { "name" : name }
```

---