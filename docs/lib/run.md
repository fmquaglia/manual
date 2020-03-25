**`app.lib.run(action=None)`** is used to execute code following a [run command from Teletype](/use/run). It takes one optional argument which specifies which decorated function to execute.

!!! Note
    From DETA lib version `21` the convention is `app.lib.run`. 
    For all earlier lib versions the convention is `app.run`. You can find a program's lib version by the `deta.lib` field in the `INFO` tab.
    The latest lib version is `22`.

**Arguments**

* `action`: `str` indicates which **`app.lib.run()`** function to execute.


<br />

**Usage example:**

```python
from deta.lib import app

@app.lib.run()
def main_handler(event):
    return "Willkommen in Berlin."

@app.lib.run("kreuzberg")
def main_handler(event):
    return "Willkommen in Kreuzberg!"

@app.lib.run("steglitz")
def main_handler(event):
    return "Willkommen in Steglitz!"
```

<br />

**Command (Teletype Studio)**
```ruby
run
```

**Command (Teletype Dash)**
```ruby
prog_name
```

**Response**
```python
"Wilkommen in Berlin!"
```

<br />

**Command (Teletype Studio)**
```ruby
run kreuzberg
```

**Command (Teletype Dash)**
```ruby
prog_name kreuzberg
```

**Response**
```python
"Wilkommen in Kreuzberg!"
```

<br />

**`event` attributes**

* `event.json`: `dict` provides the json payload as a Python dict.
* `event.body`: `str` provides the raw json payload.
* `event.type`: `str` will be instantiated to `#!py "run"`.
* `event.action`: `str` bears the action provided by the user or an empty string if no action is provided.

**Responses**

See [primitive responses](/lib/responses#primitive-responses).