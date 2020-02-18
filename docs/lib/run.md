To run your program from TeleType (the Command Line), you need to use the `app.run` decorator on the corresponding function.
This is very useful to create command line applications and scripts that you can share with your team.

**`app.run(action)`** takes one optional parameter:

* `action`: `string` which enables a user to trigger different code blocks from the DETA Teletype.


##### code

```python
from deta.lib import app

@app.run()
def main_handler(event):
    return "Welcome to Berlin"
```

##### command
```ruby
run
```

##### response
```json
"Welcome to Berlin"
```

Having different functions you could trigger is a great feature. We can achieve that by defining a corresponding `action`:


##### code
```python
@app.run(action="kreuzberg")
def kreuzberg_handler(event):
    return "Welcome to Kreuzberg"

@app.run(action="steglitz")
def steglitz_handler(event):
    return f"Welcome to Steglitz"
```

This program now will return different values from the DETA Teletype depending on the command:

##### command
```ruby
run kreuzberg
```
##### response
```json
"Welcome to Kreuzberg"
```

##### command
```ruby
run steglitz
```
##### response
```json
"Welcome to Steglitz"
```

## `event` attributes

**`event.json`**: provides the json payload as a Python dict.
**`event.body`**: raw json payload.
**`event.type`**: should be `"run"` when triggered using Teletype CLI.
**`event.action`**: should bear the action provided by the user or empty string if no action is provided.