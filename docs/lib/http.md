
The DETA library provides a small Flask-inspired http router. For a more complete http router, consider using [an external framework in your DETA program](/web_frameworks/) such as [starlette](https://www.starlette.io/), [FastAPI](https://fastapi.tiangolo.com/), [Flask](https://palletsprojects.com/p/flask/), or [Django](https://www.djangoproject.com/).


**`app.lib.http(route, methods=None)`** takes two arguments which specify the decorated function to execute following an [HTTP request](/use/http).

!!! Note
    From DETA lib version `21` the convention is `app.lib.http`. 
    For all earlier lib versions the convention is `app.http`. You can find a program's lib version by the `deta.lib` field in the `INFO` tab.

**Arguments**

* `route`: `str` which specifies the path for a corresponding HTTP request. Examples: `#!py "/"`, `#!py "/hello"`. 
    * This argument is *required*.
* `methods`: `list` of HTTP methods which can trigger the function. 
    * Defaults to all the standard HTTP methods. 
    * Example: `#!py ["GET", "PUT"]`.

**Responses**

Refer to [Responses docs](/lib/responses).

<br />

**Usage Example**

```python
from deta.lib import app

@app.http("/", methods=["GET"])
def get_handler(event):
    name = event.params.get("name")
    return {"greeting": f"Hallo, {name}!"}

@app.http("/kiez/", methods=["POST"])
def post_handler(event):
    kiez = event.json.get("kiez")
    return f"Your favorite Kiez in Berlin is {kiez}."
```

<br />

**Request-Response Pairs**

*Request*
```shell
GET app.deta.sh/<prog_path>/?name=Beverly
```

*Response*
```json
{"greeting": "Hallo, Beverly!"}
```

<br />

*Request*
```shell
POST app.deta.sh/<prog_path>/kiez/
```


with payload:
```json
{
    "kiez": "Akazienkiez"
}
```

*Response*
```json
"Your favorite kiez in Berlin is Akazienkiez."
```

<br />

**`event ` attributes**

- `event.type` : `str` instantiated to `#!py "http"`
- `event.method`: `str` the  HTTP method.
- `event.path`: `str` the HTTP path.
- `event.headers`: `dict` the HTTP headers.
- `event.params`: `dict` the HTTP query string parameters.
- `event.content_type`: `str` the value from the `Content-Type` header.
- `event.isb64`: `bool` `#!py True` if body is base64 encoded.
- `event.json` : `dict` provides the json payload as a Python dict.
- `event.cookies` : `dict` the HTTP cookies.