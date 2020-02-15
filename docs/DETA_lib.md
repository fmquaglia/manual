# The DETA Library


In addition to the [DETA router](/DETA_router.md), the DETA library provides many useful modules to give your programs extra power.

!!! Note

    `deta.lib` is under heavy development. Current version is `8`. To use the current version run this in the DETA Teletype:
    `lib use 8`

### How to import from the DETA Library

    from deta.lib import <module>
    from deta.lib.responses import <module>

## Available Modules

### Input Schema

A program's input schema describes parameters that can be passed with a program's execution.

An Input Schema is create by importing `fields` from `deta.lib` and creating a class which takes `fields.Schema` as an argument.

Input parameters can be of type `Str`, `Int`, or `Bool`.

Input parameters can be accessed directly via the `event.i` object inside an `app.run()` or `app.invoke()` route (defined in the `main.py` file of a program) where an Input class is passed as an argument.

```python
from deta.lib import app, fields

class Default_Input(fields.Schema):
    """Please fill out the form."""
    name = fields.Str('Name')
    age = fields.Int('Age')
    likes_ramen = fields.Bool('Do you like ramen?')

@app.run(inp=Default_Input)
def run_handler(event):
    """The entrypoint to your program logic."""
    return {
        'name': event.i.name,
        'age': event.i.age,
        'likes_ramen': event.i.likes_ramen
    }
```

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



## Feedback

Need help, have questions, or want to give feedback?

Please send us a note! hello `@` deta `.` sh
