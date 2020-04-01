
There are two types of responses: [Primitive](#primitive-responses) and [HTTP](#http-responses).

## Primitive Responses
When returning a response for a [Teletype run command](/use/run/) (and sometimes for [HTTP](/use/http/)) you can return primitive Python types like `str`, `int`, `float`, `Decimal`, `bool`, `dict`, `list`, and `tuple` – we will take care of serializing them. If multiple values are returned, they will be converted to a list.

Examples

```python
@app.lib.run()
def run_handler(event): 
    return "Hello, space!"

@app.lib.http("/", methods=['GET'])
def get_handler(event): 
    return {"name": "Wesley", "age": 27}
```
<br />

## HTTP Responses 

In addition to returning [Primitive responses](#primitive-responses), the DETA Library provides helper classes for returning HTTP-specific responses. These include [Response](#response) (which you can customize), [JSON](#json), [HTML](#html), and [Redirect](#redirect).

To use any of these responses, first import them from `deta.lib.responses`:

```
from deta.lib.responses import <module>
```
<br />

### Response

This is the base response and can be used to return custom responses.

**`Response(content, content_type="text/plain", code=200, headers=None)`**

**Arguments**

* `content`: any JSON-serializable value.
    * this field is required.
* `content_type`: `str` –  HTTP "Content-Type" header. 
    * Optional, defaults to `#!py "text/plain"`.
* `code`: `int` – HTTP response [status code (external link)](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status). 
    * Optional, defaults to `#!py 200`.
* `headers`: `dict` – a key-value pairs of response HTTP headers and their values. 
    * Optional, defaults to `#!py {"Content-Type": "text/plain"}`

**Example**

```python
from deta.lib.responses import Response

@app.lib.http("/", methods=['GET'])
def get_handler(event): 
    return Response("A GET triggered me!", content_type="text/plain", code=200, headers=None)
```

<br />

### JSON

Inherits from [Response](#response).

**`JSON(content, content_type="application/json", code=200, headers=None)`**

**Example**

```python
from deta.lib.responses import JSON


@app.lib.http("/", methods=['GET'])
def get_handler(event): 
    response = {"name": "Wesley", "age": 27}
    return JSON(response)

@app.lib.http("/users", methods=['POST'])
def post_handler(event): 
    # parse and save user's data...
    response = {"status": "ok"}
    return JSON(response, code=201)
```
<br />

### HTML

Inherits from [Response](#response).

**`HTML(content, content_type="text/html", code=None, headers=None)`**

**Example**

```python
from deta.lib.responses import HTML


@app.lib.http("/", methods=['GET'])
def get_handler(event): 
    # it is also possible to return an SVG object the same way 
    return HTML('<h1>hello world</h1>')
```
<br />

### Redirect

For HTTP redirects.

**`Redirect(location, temp=False)`**

**Arguments**

* `location`: *required*, `str` – the target URL. 
    * Example: `#!py "https://deta.sh/"`
* `temp`: `bool`
    * `#!py False` for permanent HTTP redirect (code `#!py 301`, default)
    * `#!py True`for temporary redirect (code `302`).

**Example**

```python
from deta.lib.responses import Redirect


@app.lib.http("/", methods=['GET'])
def get_handler(event): 
    return Redirect("https://example.com/new-page", temp=True)
```