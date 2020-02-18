
### Response Types

The DETA Library also provides modules for returning common response types from DETA programs. These include `HTML`, `JSON`, and `response`.

```
from deta.lib.responses import <module>
```

#### Returning HTML

```python
from deta.lib.responses import HTML


@app.http("/", methods=['GET'])
def get_handler(event): 
    # it is also possible to return an SVG object the same way 
    return HTML('<h1>hello world</h1>')
```

#### Returning JSON

```python
from deta.lib.responses import JSON


@app.http("/", methods=['GET'])
def get_handler(event): 
    response = {"name": "Wesley", "age": 27}
    return JSON(response)
```

