

### app.cron()

`app.cron()` takes no parameters for the time being and executes the code following a scheduled execution following a DETA `cron` event.

```python
from deta.lib import app

@app.cron()
def cron_handler(event):
    return "I run on a schedule"
```

### app.cron()

#### Attributes
- `event.cron` : `bool` will be instantiated `True`
- `event.type` : `str` will be instantiated to "cron"
- `event.time` : `str` time at which the event took place