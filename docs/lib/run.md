**`app.run(action=None)`** takes one optional argument and executes the decorated functions following a [run command from Teletype](/use/run).

**Arguments**

* `action`: `str` TODO


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

**`event` attributes**

* `event.json`: `dict` provides the json payload as a Python dict.
* `event.body`: `str`raw json payload.
* `event.type`: `str` will be instantiated to `#!py "run"`.
* `event.action`: `str` bears the action provided by the user or empty string if no action is provided.

**Responses**

* [Plain Text](TODO)
* [JSON](TODO)
