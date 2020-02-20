
There are two types of responses:

## Primitive responses
When returning a response for a run command (and sometimes for HTTP) you could return primitive Python types like `str`, `int`, `float`, `Decimal`, `bool`, `dict`, `list`, and `tuple` – we will take care of serializing them. If multiple values are returned, they will be converted to a list.

Example

```python
@app.run()
def run_handler(event): 
    return "Hello, space!"

@app.http("/", methods=['GET'])
def get_handler(event): 
    return {"name": "Wesley", "age": 27}
```


## HTTP responses 

In addition to returning [Primitive responses](#primitive-responses), the DETA Library provides helper classes for returning HTTP-specific responses. These include `HTML`, `JSON`, `Redirect`, and `Response` – which you could customize.

To use any of these responses, first import them from `deta.lib.responses`:

```
from deta.lib.responses import <module>
```
### Response

This is the base response and could be used to return custom responses.

**`Response(content, content_type="text/plain", code=200, headers=None)`**

Arguments:

* `content`: *required* –  any JSON-serializable value.
* `content_type`: `str`–  HTTP "Content-Type" header. Default is `#!py "text/plain"`.
* `code`: `int` – HTTP response [status code (external link)](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status). Default is `#!py 200`.
* `headers`: `dict` – a key-value pairs of response HTTP headers and their values. Default: `#!py {"Content-Type": "text/plain"}`

### JSON

Inherits from [Response](#response).

**`JSON(content, content_type="application/json", code=200, headers=None)`**

Example

```python
from deta.lib.responses import JSON


@app.http("/", methods=['GET'])
def get_handler(event): 
    response = {"name": "Wesley", "age": 27}
    return JSON(response)

@app.http("/users", methods=['POST'])
def get_handler(event): 
    # parse and save user's data...
    response = {"status": "ok"}
    return JSON(response, code=201)
```

### HTML

Inherits from [Response](#response).

**`HTML(content, content_type="text/html", code=None, headers=None)`**

Example

```python
from deta.lib.responses import HTML


@app.http("/", methods=['GET'])
def get_handler(event): 
    # it is also possible to return an SVG object the same way 
    return HTML('<h1>hello world</h1>')
```

### Redirect

For HTTP redirects.

**`Redirect(location, temp=False)`**

Arguments:

* `location`: *required*, `str` – the target URL. Example: `#!py "https://deta.sh/"`
* `temp`: `bool` – `#!py False` for permanent HTTP redirect (code `#!py 301`, default) and `#!py True`for temporary redirect (code `302`).

Example

```python
from deta.lib.responses import Redirect


@app.http("/", methods=['GET'])
def get_handler(event): 
    return Redirect("https://example.com/new-page", temp=True)
```