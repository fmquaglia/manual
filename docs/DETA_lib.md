# The DETA Library

!!! Note

    `deta.lib` is under heavy development. Current version is `9`. To use the current version run this in the DETA Teletype:
    `lib use 9`

### How to import from the DETA Library

    from deta.lib import <module>
    from deta.lib.responses import <module>

## Available modules

### Input Schema

A program's input schema describes parameters that can be passed with a program's invocation.

Input parameters can be of type `Str`, `Int`, or `Bool`.

Input parameters can be accessed directly via the `event.i` object inside the main 'program' function (defined in the `main.py` file of a program).

```python
from deta.lib import fields

class Input(fields.Schema):
    """Please fill out the form."""
    name = fields.Str('Name')
    age = fields.Int('Age')
    likes_ramen = fields.Bool('Do you like ramen?')

def program(event):
    """The entrypoint to your program logic."""
    return {
        'name': event.i.name,
        'age': event.i.age,
        'likes_ramen': event.i.likes_ramen
    }
```
### Key-Value Store

```python
from deta.lib import Database

# instantiate a simple database
books = Database() 
# giving a name is optional: Database('books'). 

books.put('my_key', 'my_val')  
# values can be: int, str or Decimal
# lists & dicts that contain only mentioned types are also supported

# 'books.put' overrides the value if the key already exists. 
# 'books.add' will not override the value (but will raise a KeyError)

# get all books:
books.all()

# get one book
books.get('my_key')

# delete a book
books.delete('my_key')
```
     

### File Storage
```python
from deta.lib import files

# store a file
files.put('filename.ext', file_content)
# content can be bytes, string or a file object

# get a file
files.get('filename.ext')

# delete a file
files.delete('filename.ext')

# list files
files.list()
```
### Rendering/returning HTML
```python
from deta.lib.responses import HTML

def program(event):
    # it is also possible to return an SVG object the same way 
    return HTML('<h1>hello world</h1>')
```
### Simple Router

DETA ships with a simple router for the methods `GET` and `POST`.

These methods can be invoked on the program specific url `<program_url>`.

DETA does not support path-based routing yet (like `/some/deep/path`). 

Requests will be routed to the user defined `GET` or `POST` function by type.
```python
from deta.lib import router

@router.get()
def myget(event):
    return 'i got a get'

@router.post()
def mypost(event):
    return 'i got a post'

def program(event):
    return router.serve(event)
```

#### GET Requests
Data can be passed to a DETA program with a `GET` request using query parameters:
```
<program_url>?school=Bauhaus&city=Weimar
```

The values are inside the `event.params` object, accesible via the `get` method.
```python
from deta.lib import router

@router.get()
def myget(event):
    school = event.params.get('school')
    city = event.params.get('city')
    return f"I studied at {school} in {city}"

def program(event):
    return router.serve(event)
```
#### POST Requests

Data can be passed to a DETA program with the `POST` route, using a JSON payload.

```JSON
{
    "id": "7",
    "name": "Ludwig"
}
```

The values are accessible via the `event.body` object.

```python
from deta.lib import router, Database

students = Database('enrollment')

@router.post()
def mypost(event):
    student_id = event.body['id']
    name = event.body['name']
    students.put(student_id, name)
    return students.all()

def program(event):
    return router.serve(event)
```

#### HTTP-Endpoint

The DETA console provides a view where GET requests can be made on a program.

The URL bar in the program's GET view contains the program's URL.

- Only `GET` and `POST` methods are allowed on this endpoint.

User defined query parameters can be added to the GET request.

### Load (RPC)

DETA programs can call other DETA programs (by default within the same space).

A caller program can pass arguments to a callee (as outlined in the callee's input schema).

To load the callee program into the caller program, pass the callee's program id (found in the `INFO` tab of an open program) as a string into the load module.

```python
from deta.lib import load

otherprogram = load('<program_id>')

def program(event):    
    return otherprogram(greeting='noice')  # otherprogram takes `greeting` arg
```

### Email

DETA programs have their own unique email address.

```python
from deta.lib import send_email


def program(event):
    send_email('email', 'subject', 'body')
    return
```


## Feedback

Need help, have questions, or want to give feedback?

Please send us a note! hello `@` deta `.` sh
