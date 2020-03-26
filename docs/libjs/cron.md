**`app.lib.cron()`** takes no parameters and executes the decorated function following a [scheduled execution](/use/cron).

!!! Note
    From DETA lib version `21` the convention is `app.lib.cron`. 
    For all earlier lib versions the convention is `app.cron`. You can find a program's lib version by the `deta.lib` field in the `INFO` tab.
    The latest lib version is `22`.

**Usage example:**

```python
from deta.lib import app

@app.lib.cron()
def cron_handler(event):
    print("I run on a schedule")
    return "done"
```

**`event` attributes:**

- `event.type` : `str` will be instantiated to `#!py "cron"`.
- `event.time` : `str` time at which the event took place.
