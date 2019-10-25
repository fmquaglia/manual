!!! Note

    `deta.lib` is under heavy development. Current version is `16` to use the current version run this in the command line:
    `lib use 4`

## How to import from the SDK

    from deta.lib import <module>

## Available modules

### Email

`send_email('email', 'subject', 'body')`

### SMS

`sms('+000000', 'message')`

### Key-Value Store
```python
from deta.lib import Database

# instantiate a db
books = Database() # giving a name is optional: Databse('books'). 
# the program's name will be used as name by default.
# you also can re use another database by instantiating 
# it with the program id or provided name: 
users = Database('users')
notes= Database('<id_of_notes_program>')

books.put('mykey', {'my': 'val'})  # value can be: int, str or Decimal
# also lists, dicts that can only contain mentioned types

# the 'books.put' method overides value if key already exists. 
#use 'books.add' to prevent overriding value (will raise KeyError)

# get all books:
books.all()

# get one book
books.get('mykey')

# delete a book
books.delete('mykey')
```

### Input schema/ UI schema

    from deta.lib import fields
    
    # only 2 types are supported at the moment: fields.Str, fields.Int & fields.Bool
    @schema
    class Input:
        name = fields.Str('Name', default='example')
        age = fields.Int('Your age')
    		cool = fields.Bool('Are you cool?')
    
    # inside the main program, you can access the input direclty via the event.i object
    # event.i.name, ...
    def program(event):
        print(event.i.name) # => "alex" (if input was provided)
     

### File Storage

    from deta.lib import files
    
    # store a file
    files.put('filename.ext', file_content)
    # content could be bytes, string or a file object
    
    # get a file
    files.get('filename.ext')
    
    # delete a file
    files.delete('filename.ext')
    
    # list files
    files.list()

### Rendering/returning HTML

    from deta.lib.responses import HTML
    
    def program(event):
    		# it is also possible to return an SVG object the same way 
        return HTML('<h1>hello world</h1>')

### Simple Router

Deta ships with a simple router for the Methods `GET` and `POST` 

Deta does not support path-based routing yet (like `/some/deep/path`). 

Requests will be routed to the `POST` or `GET` functions.

    from deta.lib import router
    
    @router.get()
    def myget(event):
        return 'i got a get'
    
    @router.post()
    def mypost(event):
        return 'i got a post'
    
    def program(event):
        return router.serve(event)

To be able to pass-through extra data to your function (e.g. to the `GET` route), you should use query parameters.

`https://dev.deta.sh/<id>?occupation=poet&noice=true`

The values are inside the `event.params` object.

    from deta.lib import router
    
    @router.get()
    def myget(event):
    		occupation = event.params.get('occupation')
        return f"I'm a {occupation} and I didn't event realize that."
    
    def program(event):
        return router.serve(event)

### Calling another program

    from deta.lib import load
    
    otherprogram = load('<program_id>')
    
    def program(event):    
        return otherprogram(greeting='noice')  # otherprogram takes `greeting` arg

## Send messages to your dashboard

    from deta.lib import dash
    
    def program(event):
    		dash('my message')  # simple message
    		
    		#  you can send a message to a specifc inbox. Default is the program's name.
    		dash('my info', 'general') 
    		
    		# or add a message level (options: 0=info, 1=warning and 2=error). default: info
    		# levels are color-coded
    		dash('my warning', 'alerts', 1)
    		
    		# to pass a level without providing channel, just pass `None` instead.
    		dash('Something is wrong!', None, 2)
    		return {'message': 'cool'}

# HTTP-Endpoint

You can get your program's URL by replacing `<id>` in the following:

[https://dev.deta.sh/](https://dev.deta.sh/deta-dev-program-)<id>

With the `id`from the console. The id is a long string.

Example:

![](id-1e9a7ab5-7249-4be3-ad4e-e4db6a180bb7.png)

URL:

[**https://dev.deta.sh/](https://dev.deta.sh/deta-dev-program-)b8b7f853-f38e-8736-aaca-4b3dd665afd5**

- Only `GET` and `POST` methods are allowed. (see [Simple Router](https://www.notion.so/DETA-Manual-a175bc23f7004d2481f2d21ca926e8d9#d8fbc751089743f8a730cd8a2afdbf5b))
- **Endpoints are public!!!!**

~~When a program is triggered via the http endpoint, you will find the request data in the `event` argument itself. Also `event.is_http` will be set to `True`~~

~~Try this in your program to find out what data is hidden in `event`~~

# Dasboard

As of recently, Deta offers a personal graphical dashboard available under:

> [https://web.deta.sh/dash](https://web.deta.sh/dash)

You can  also open it by typing `dash` in the console (Teletype).

You can send messages to your dashboard from your programs. Read the details in this `deta.lib` section.