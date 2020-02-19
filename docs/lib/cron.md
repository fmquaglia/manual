**`app.cron()`** takes no parameters and executes the decorated function following a [scheduled execution](/use/cron).

**Usage example:**

```python
from deta.lib import app

@app.cron()
def cron_handler(event):
    print("I run on a schedule")
    return "done"
```

**`event` attributes:**

- `event.type` : `str` will be instantiated to `#!py "cron"`.
- `event.time` : `str` time at which the event took place.
