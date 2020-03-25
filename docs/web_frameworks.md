
DETA is an extremely fast way to get a web framework up and running, supporting most Python web frameworks out of the box.

We tested the following frameworks:

- Flask
- Django
- FastAPI
- Sanic
- Starlette

DETA understands both WSGI and ASGI interfaces and you should be able to run other frameworks without any issues.


### How to

running a web framework on DETA requires two simple steps.

#### 1) Install the Framework

Open a DETA program and [install the framework dependency](/packages/) using `pip` in the [Studio Teletype](/teletype/).

```pip install <framework_name>```

#### 2) Instantiate your web app with the name `app`

It is necessary that the framework is instantiated in a variable named `app`
to work correctly.

The example below uses FastAPI but the convention is universal.

```python
from fastapi import FastAPI

# This is a regular FastAPI app. Read the docs of FastAPI:
# https://fastapi.tiangolo.com/

app = FastAPI()

@app.get("/")
async def get_handler():
    return {"message": "hello from DETA + FastAPI"}
```
<br />

### Using a third-party framework and deta.lib simultaneously

Using `@app.lib` decorators (run and cron) alongside a framework in a single DETA program is possible.

To do so, import `App` from `deta.lib` and instantiate your framework inside it

```python
from deta.lib import App
from fastapi import FastAPI

# This is a regular FastAPI app. Read the docs of FastAPI:
# https://fastapi.tiangolo.com/

app = App(FastAPI())

@app.get("/")
async def get_handler():
    return {"message": "Hello from DETA + FastAPI"}

@app.lib.run()
def handler(event):
    return "Hello from the Teletype"
```


### Getting FastAPI docs working:

Add your program path when you instantial a `FastAPI`app:

example:

```python
app = FastAPI(openapi_prefix="/rzzj7f2jw5ih")
```

### Running Django

We suggest you use a minimal Django setup to reduce unnecessary file bulk -- following is a minimal Django app that runs inside DETA:

```python
import sys
from django.conf import settings
from django.conf.urls import url
from django.core.wsgi import get_wsgi_application
from django.http import JsonResponse

settings.configure(
    DEBUG=True,
    ROOT_URLCONF=sys.modules[__name__],
)

def index(request):
    return JsonResponse({"Hello": "World"})

urlpatterns = [
    url(r'^$', index),
]


app = get_wsgi_application()
```
### Things to note

- As you can see we expect an `app` object in `main.py`.
- We take care of forwarding HTTP requests to oyu -- no servers, sockets or ports to listen to.
- The file system is read-only except `/tmp`, to which you could write data but it ephemeral and not consistant across API calls. 