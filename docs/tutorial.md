In this short tutorial, we will learn how the basics of DETA by creating a simple program to help you manage your to-dos.

## 1) Creating a program

The simplest way to create a program on DETA is by going to the [Studio](https://web.deta.sh/studio) and entering the `new {myprogram}` command into the Teletype (aka cli).


Program names are composed of alphanumerical characters and underscores `_`. Spaces and other symbols are not supported.

!!! Note
    We currently only support **Python 3.7** programs but JavaScript is underway.

Here, we're creating a program called `mytodos`

##### Command
```ruby
new mytodos
```

It takes _less than 1 second_ to create the program – the code should come back looking something like this:

##### Code
```python
from deta.lib import app

@app.run()
def runner(event):
    name = event.json.get('name', 'there')
    return f"Hello, {name}!"
```

!!! Note
    The **`@app.run()`** we're importing and using is essential for running out code. You will learn more about it in (TODO).

**Our *tiny* program:**

- Can auto-scale to millions of invocations.
- Is secure and production-ready.
- Has built-in authentication and permissions management.
- Has a config-less API, and an Email address.
- Has instant access to managed Databases, Cloud Files, Cron and much more.

## 2) Running our program

DETA gives you many ways to interact with your program. For now we will use our built in command line that we call "Teletype"

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

As you can see, we send your keyword arguments as a JSON payload when invoking the program from Teletype.

## 3) Updating the code

Making changes to our program is really straight forward; just enter `deploy` into Teletype.
Alternatively hit `cmd+s` or `ctr+s` when inside the editor.

Let's change our current program to accept to-do specific input:

##### Code

```python
from deta.lib import app

@app.run()
def runner(event):
    text = event.json.get("text")  # String value
    urgent = event.json.get("urgent", False)  # Boolean value
    return {
        "name": name,
        "urgent": urgent
    }
```
Then deploy:

##### Command
```ruby
deploy
```

Then run:

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


Lets try with an urgent task:

 

```ruby
run --text "Drink coffee" -urgent
```

response:

```json
{
    "text": "Drink coffee",
    "urgent": true
}
```

## Storing Data

We saw how we can pass data to our program, let's learn how to permanently store them.


DETA gives you (your program) the ability to use Databases on the fly, you don't even need to create them!

Here's how it works:

1. **Import** the `Database` helper class from `deta.lib`.
2. **Initialize** a DB.
3. **Use** the DB.

##### code
```python
from deta.lib import app, Database  # 1) Import

todos = Database()  # 2) Initialize 

@app.run()
def runner(event):
    key = event.json.get("key")  # using a manual key for simplicity
    text = event.json.get("text")
    urgent = event.json.get("urgent", False)
    
    if not key or not text:
        return "missing fields"

    todo = {
        "text": text,
        "urgent": urgent
    }

    todos.put(key, todo)  # 3) Use
    return todos.all()
```

let's deploy again:

##### Command
```ruby
deploy
```

Then run the command from the previous steps:

##### Command
```ruby
run --text "Do the dishes" --key 1
```
The response form our program, which is fetching all the items in the database via `todos.all()`

##### Output
```json
[
    {
        "key": "1",
        "data": {
            "urgent": false,
            "text": "Do the dishes"
        }
    }
]
```

Lets try again with the urgent task:

```ruby
run --text "Drink coffee" --key 2 -urgent
```

response:

```json
[
    {
        "key": "1",
        "data": {
            "urgent": false,
            "text": "Do the dishes"
        }
    },
    {
        "key": "2",
        "data": {
            "urgent": true,
            "text": "Drink coffee"
        }
    }
]
```

!!! Info
    There's no limit to the number of Databases you can initialize with DETA. Feel free to use multiple of them to store different items.

        db = Database()
        customers = Database("customers")
        debug_db_delete_me = Database("or_not")

    We won't charge you based on the DBs you have, rather data storage. Don't worry for now, it's free.

## Extending our run

In the previous section, the same function creates the tasks and show us the existing to-dos in our database.
Let's split TODO

```python
from deta.lib import app, Database  # 1) Import

todos = Database()  # 2) Initialize 

@app.run()
def runner(event):
    key = event.json.get("key")  # using a manual key for simplicity
    text = event.json.get("text")
    urgent = event.json.get("urgent", False)
    
    if not key or not text:
        return "missing fields"

    todo = {
        "text": text,
        "urgent": urgent
    }

    todos.put(key, todo)  # 3) Use
    return f"Added '{text}'"

@app.run("list")
def todos_list(event):
    return todos.all()
```

Now if we add a new task:

##### code
```ruby
run --text "Go to sleep" --key 3
```

We will get this response instead:

##### output
```json
"Added 'Go to sleep'"
```

And we can see the todos in our DB by running:

```ruby
run list
```

```json
[
    {
        "key": "1",
        "data": {
            "urgent": false,
            "text": "Do the dishes"
        }
    },
    {
        "key": "2",
        "data": {
            "urgent": true,
            "text": "Drink coffee"
        }
    },
    {
        "key": "3",
        "data": {
            "urgent": false,
            "text": "Go to sleep"
        }
    }
]
```

The keyword we provided after `run` – in this case it was `list` – is what we call a **Run Action**, it enables us to create powerful command line applications in a simple matter.

Let add a piece of Python of to make our returned Tasks look nicer:

```python
def format_todos(todos):
    rows = list()
    for todo in todos:
        key = todo["key"]
        text = todo["data"]["text"]
        urgent = " (Urgent)" if todo["data"]["urgent"] else ""
        row = f"{key}: {text}{urgent}"
        
        rows.append(row)
    return rows
```

And use it in our `todos_list` function:

```python
@app.run("list")
def todos_list(event):
    return format_todos(todos.all())
```


lets run list again:

##### code
```ruby
run list
```

##### output
```json
[
    "1: Do the dishes",
    "2: Drink coffee (Urgent)",
    "3: Go to sleep"
]
```

<!-- Let's add some Python functions to auto generate the keys for us, so we don't have to provide them manually:

Add this piece of code at the top of your program, after  -->