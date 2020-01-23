# App Router

The DETA router provides a blueprint outlining which blocks of code will be run by which triggers.

The basic router is implemented by importing `app` from `deta.lib`.

`app` has four basic methods which route four different types of incoming requests to different code blocks.

These methods are:

1. `run`: handles code triggered from the [DETA Teletype](teletype.md).
2. `http`: handles code triggered from an HTTP request.
3. `cron`: handles code triggered from a scheduled execution.
4. `invoke`: handles code triggered from another DETA program.

```python
from deta.lib import app

@app.run()
def run_handler(event):
    return "runs when this program is triggered from the DETA Teletype"

@app.http("/", methods=["GET"])
def http_handler(event):
    return "runs when I hit this program's endpoint with an HTTP GET"

@app.cron()
def cron_hanlder(event):
    return "runs when I schedule this program"

@app.invoke()
def invoke_handler(event):
    return "runs when a another program calls this program"
```

Each method takes different parameters and handles the `event` object differently. The details of this are handled at the [bottom of the page](#event-details).

### app Methods

### app.run()

`app.run()` takes two optional parameters:

1. `action`: `string` which enables a user to trigger different code blocks from the DETA Teletype.
2. `inp`: `string` which maps arguments of the event object to a user defined Input Schema, making these arguments accesible via the `event.i` object.

```python
from deta.lib import app, fields

class User(fields.Schema):
    """Please fill out the form."""
    name = fields.Str('Name')
    age = fields.Int('Age')

@app.run(inp=User)
def kreuzberg_handler(event):
    name = event.i.name
    age = event.i.age
    return f"{name} is {age} and developing DETA apps out of Berlin"

@app.run(action="kreuzberg", inp=User)
def kreuzberg_handler(event):
    name = event.i.name
    age = event.i.age
    return f"{name} is {age} and developing DETA apps out of Kreuzberg"

@app.run(action="steglitz", inp=User)
def steglitz_handler(event):
    name = event.i.name
    age = event.i.age
    return f"{name} is {age} and developing DETA apps out of Steglitz"
```

This program now will return different values from the DETA Teletype depending on the command:

```shell
run --name wesley --age 27
```

```json
"wesley is 27 and developing DETA apps out of Berlin"
```

<br />

```shell
run kreuzberg --name beverly --age 43
```

```json
"beverly is 43 and developing DETA apps out of Kreuzberg"
```

### app.http()

`app.http()` takes two parameters:

1. The first parameter is a `string` which specifies the `path` which the HTTP request hits.
2. `methods`: takes an array which specify which HTTP methods will trigger the code block.

```python
from deta.lib import app

@app.http("/", methods=["GET"])
def get_handler(event):
    name = event.params.get('name')
    age = event.params.get('age')
    return f"{name} is {age} and developing DETA apps out of Berlin"

@app.http("/kreuzberger/", methods=["GET"])
def kreuzberg_get_handler(event):
    name = event.params.get('name')
    age = event.params.get('age')
    return f"{name} is {age} and developing DETA apps out of Kreuzberg"

@app.http("/steglitzer/", methods=["POST"])
def steglitz_post_handler(event):
    name = event.json['name']
    age = event.json['age']
    return f"{name} is {age} and developing DETA apps out of Steglitz"
```

In the above example, hitting the program with an HTTP request will do different things, depending on route and HTTP method.

<br />

*Request*
```shell
GET on.deta.dev/<prog_path>/?name=Beverly&age=43
```

*Response*
```json
"Beverly is 43 and developing DETA apps out of Berlin"
```

<br />

*Request*
```shell
GET on.deta.dev/<prog_path>/kreuzberger/?name=Beverly&age=43
```

*Response*
```json
"Beverly is 43 and developing DETA apps out of Kreuzberg"
```

<br />

*Request*
```shell
POST on.deta.dev/<prog_path>/steglitzer/
```

with payload:
```json
{
    "name": "Wesley",
    "age": 27
}
```

*Response*
```json
"Wesley is 27 and developing DETA apps out of Steglitz"
```


### app.cron()

`app.cron()` takes no parameters for the time being and executes the code following a scheduled execution following a DETA `cron` event.

```python
from deta.lib import app

@app.cron()
def cron_handler(event):
    return "I run on a schedule"
```

### app.invoke()

`app.invoke()` takes the same parameters as `app.run()`.

```python
from deta.lib import app, fields

class User(fields.Schema):
    """Please fill out the form."""
    name = fields.Str('Name')
    age = fields.Int('Age')

@app.invoke(inp=User)
def invoke_handler(event):
    name = event.i.name
    age = event.i.age
    return f"Another DETA program called me and passed me {name} who is {age}"

@app.invoke(action="kreuzberg", inp=User)
def invoke_handler(event):
    name = event.i.name
    age = event.i.age
    return f"Another DETA program called me and passed me {name} who is {age} and is making DETA apps out of Kreuzberg"
```


## Event Details

All events, regardless of the `app` method have:

- `event.body` the body of the event (a string)

### app.run() & app.invoke()

#### Attributes:
- `event.run`: `bool` will be instantiated to `True`
- `event.type`: `str` will be instantiated as "run"
- `event.action`: `str` the action defined in the handling function, will be an empty string if not defined 

#### Property:
- `event.json`: `dict` The json representation of `event.body` as a Python dict.

#### Inputs:
- `event.i`: `object` Input to the function according to the schema, only available if an input is provided to the funtion. Can access fields as attributes.

### app.cron()

#### Attributes
- `event.cron` : `bool` will be instantiated `True`
- `event.type` : `str` will be instantiated to "cron"
- `event.time` : `str` time at which the event took place

### app.http()

#### Attributes
- `event.http`: `bool` instantiated to `True`
- `event.type` : `str` instantiated to "http"
- `event.method`: `str` the http method in the request 
- `event.path`: `str` the path of the resource in the request
- `event.headers`: `dict` http headers  
- `event.params`: `dict` the query string params
- `event.content_type`: `str` the value in the header `Content-Type` in the request, is an empty string if header not present
- `event.isb64`: `bool` if body is base64 encoded, body is decoded by the DETA library if is `True`

#### Properties
- `event.json` : `dict` json representation of the the event body
- `event.cookies` : `dict` cookies in the request if present

## Feedback

Need help, have questions, or want to give feedback?

Please send us a note! hello `@` deta `.` sh