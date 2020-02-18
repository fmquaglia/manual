
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
