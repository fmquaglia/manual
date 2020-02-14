# Getting Started

In this short tutorial, we will learn how to use DETA by creating a simple program to help you manage your to-dos.

## 1) Creating a program

The simplest ways to create a program on DETA is by going to the [Studio](https://web.deta.sh/studio) and typing the `new` command followed by the name of the program in the cli. `fixme`


Program names are composed of alphanumerical characters and underscores `_`. Spaces and symbols are not supported.

!!! Note
    We currently only support **Python 3.7** but JavaScript is underway.
Here, we're creating a program called `mytodos`

##### Command
```ruby
new mytodos
```

It takes _less than 1 second_ to create the program – the code should look something like this:

##### Code
```python
from deta.lib import app

@app.run()
def runner(event):
    name = event.json.get('name', 'there')
    return f"Hello, {name}!"
```

!!! Note
    For now lets ignore  both `from deta.lib import app`and the `@app.run()` decorator. `fixme`

Do not let the simplicity fool you, this tiny program:

- Can auto-scale to millions of invocations.
- Is secure and production-ready.
- Has built-in authentication and permissions management.
- Has a config-less API, and an Email address.
- Instant access to managed Databases, Cloud Files, Cron and much more.

## 2) Run!

Deta offers many ways to interact with your program. For now we will use our built in command line that we call "Teletype"

##### Command

```ruby
run
```

Watch the "CONSOLE" on right side for the response:

##### Output
```json
"Hello, there!"
```

Now lets try providing our program with a keyword argument.
##### COMMAND
```ruby
run --name Geordi
```

Watch the response: 

##### Output
```json
"Hello, Geordi!"
```

## 3) Update the code

Making changes to our program is really straight forward; just type `deploy` in Teletype.
You could also his `cmd+s` or `ctr+s` when inside the editor.

Let's change our current program to accept to-do specific input:

##### Code

```python
from deta.lib import app

@app.run()
def runner(event):
    text = event.json.get("text")
    urgent = event.json.get("urgent", False)
    return {
        "name": name,
        "urgent": urgent
    }
```
... then deploy:

##### Command
```ruby
deploy
```
... then run
##### Command
```ruby
run --text "Do the dishes"
```

##### Output
```json
{
    "text": "Do the dishes",
    "urgent": false
}
```


Lets try with an urgent one:

 

    run --text "Drink coffee" -urgent

response:

    {
        "text": "Drink coffee",
     **   "urgent": true
    }

## Using Database (modules)

Wouldn't it be convenient to store whos joining our mission:

Two steps:

1.  just import `Database` from `deta.lib` 
2. Use it.

    from deta.lib import app, Database
    
    todos = Database()
    
    @app.run()
    def runner(event):
    		key = event.json.get("key")  # manual key for simplicity
        text = event.json.get("text")
        urgent = event.json.get("urgent", False)
        
        if not key or not text:
            return "missing fields"
    
        todo = {
            "text": text,
            "urgent": urgent
        }
    
        todos.put(key, todo)  # using name as a key to make our code simple
        return todos.all()

There's no limit to the number of databases blah

    db = Database()
    customers = Database("customers")
    debug_db_delete_me = Database("or_not")

We won't charge you based on the DBs you have, rather data storage. don't worry for now, its free.

## Extending our run

What if we want to see the members already in our db

Add this to the end of your file:

    @app.run("list")
    def members(event):
        return todo.all()