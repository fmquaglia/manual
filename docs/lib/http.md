
<<<<<<< HEAD
DETA SDK provides a small Flask-inspired http router.
=======
DETA Library provides a small web http router very similar to the one provided by Flask.
>>>>>>> 2020-docs


**`app.http(route, methods=None)`** takes two arguments which specify the decorated function to execute following an [HTTP request](/use/http).

**Arguments**

* `route`: `str` which specifies the path for a corresponding HTTP request. Examples: `#!py "/"`, `#!py "/hello"`. 
    * This argument is *required*.
* `methods`: `list` of HTTP methods which can trigger the function. 
    * Defaults to all the standard HTTP methods. 
    * Example: `#!py ["GET", "PUT"]`.

<br />

**Usage Example**

```python
from deta.lib import app

@app.http("/", methods=["GET"])
def get_handler(event):
    name = event.params.get("name")
    return {"greeting": f"Hallo, {name}!"}

@app.http("/steglitzer/", methods=["POST"])
def post_handler(event):
    kiez = event.json.get("kiez")
    return f"Your favorite Kiez in Berlin is {kiez}."
```

**Responses**

Refer to [Responses docs](/lib/responses).

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