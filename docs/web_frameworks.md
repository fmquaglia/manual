
DETA is an extremely fast way to get a web framework deployed, supporting both ASGI and WSGI web frameworks out of the box.

Deploying a web framework on DETA requires two simple steps.

### Install the Framework

Open a DETA program and [install the framework dependency](/packages/) using `pip` in the [Studio Teletype](/teletype/).

```pip install <framework_name>```

### Instantiate an 'app' variable containing the framework

It is necessary that the framework is instantiated in a variable named `app`
to work correctly.

From this point, the framework can be used normally and executes deployed code.

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

#### Compatibility with the DETA app.lib decorators

Dual-compatibility with the DETA `@app.lib` decorators (run and cron) alongside a framework in a single DETA program is possible.

To do so, import `App` from `deta.lib` and wrap `App` around the framework in the instantiation of `app`.

```python
from deta.lib import App
from fastapi import FastAPI

# This is a regular FastAPI app. Read the docs of FastAPI:
# https://fastapi.tiangolo.com/

fast = FastAPI()

app = App(fast)

@app.get("/")
async def get_handler():
    return {"message": "Hello from DETA + FastAPI"}

@app.lib.run()
def handler(event):
    return "Hello from the Teletype"
```