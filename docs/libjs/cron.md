**`app.lib.cron()`** takes a function and executes following a [scheduled execution](/use/cron).

**Usage example:**

```javascript
const {app} = require('detalib');

app.lib.cron(async event => 'I run on a schedule');

export.modules = app;
```

**`event` attributes:**

- `event.type` : `String` will be instantiated to `'cron'`.
- `event.time` : `String` time at which the event took place.
