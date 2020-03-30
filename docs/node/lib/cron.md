**`app.lib.cron(func)`** takes a function and executes following a [scheduled execution](/use/cron).

**Arguments**

* `func`: `Function` function to be executed.


**Usage example:**

```javascript
const { app } = require('detalib');

app.lib.cron(event => 'I run on a schedule');

export.modules = app;
```

**`event` attributes:**

* `event.type` : `String` will be instantiated to `'cron'`.
* `event.time` : `String` time at which the event took place.
