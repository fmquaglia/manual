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

### Invoke (RPC)

DETA programs can call other DETA programs (by default within the same space).

A caller program can pass arguments to a callee.

To load the callee program into the caller program, pass the callee's program id (found in the `INFO` tab of an open program) as a string into the `invoke` module.

#### Caller Program

```python
from deta.lib import app, invoke

otherprogram = invoke('<program_id>')

@app.run()
def run_handler(event):    
    return otherprogram(action="kreuzberg", name='Wesley', age=27)  # otherprogram takes a `name` & 'age' args and has an action handler

@app.run(action="steglitz")
def steglitz_run_handler(event):    
    return otherprogram(action="steglitz", name='Wesley', age=27)  # otherprogram takes a `name` & 'age' args and has an action handler
```

#### Callee Program

```python
from deta.lib import app, fields

class User(fields.Schema):
    name = fields.Str('name')
    age = fields.Int('age')

@app.invoke(action="kreuzberg")
def invoke_handler(event): 
    name = event.json['name']
    age = event.json['age']
    return f"Another DETA program called me and passed me {name} who is {age} and is making DETA apps out of Kreuzberg"

@app.invoke(action="steglitz", inp=User)
def steglitz_invoke_handler(event): 
    name = event.i.name
    age = event.i.age
    return f"Another DETA program called me and passed me {name} who is {age} and is making DETA apps out of Steglitz"
```

### Email

DETA programs have their own unique email address.

```python
from deta.lib import app, send_email


@app.run()
def run_handler(event): 
    send_email('email', 'subject', 'body')
    return
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
