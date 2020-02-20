**`app.run(action=None)`** is used to execute code following a [run command from Teletype](/use/run). It takes one optional argument which specifies which decorated function to execute.

**Arguments**

* `action`: `str` indicates which **`app.run()`** function to execute.


<br />

**Usage example:**

```python
from deta.lib import app

@app.run()
def main_handler(event):
    return "Willkommen in Berlin."

@app.run("kreuzberg")
def main_handler(event):
    return "Willkommen in Kreuzberg!"

@app.run("steglitz")
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