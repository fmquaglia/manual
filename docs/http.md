
`deta.lib` provides you with a small web http router very similar to the one provided by Flask.


**`app.http(route, methods)`** takes two parameters:

* `route`: required `string` which specifies the `path` which the HTTP request hits, e.g `"/"` or `"/hello"`.
* `methods`: takes a list of HTTP methods will trigger the code block (e.g. `["GET", "PUT"]`), default is all the standard HTTP methods.

Examples

```python
from deta.lib import app

@app.http("/", methods=["GET"])
def get_handler(event):
    name = event.params.get('name')
    age = event.params.get('age')
    return f"{name} is {age} and developing DETA apps out of Berlin"
```

```python
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