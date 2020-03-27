**`app.lib.run(func, action)`** is used to execute code following a [run command from Teletype](/use/run). It takes name of the action and the function to be executed.

**Arguments**

- `func`: `Function` indicates which function to execute when `action` is passed

- `action`: `String` indicates which **`app.lib.run()`** function to execute.

<br />

**Usage example:**

```javascript
const { app } = require('detalib');

app.lib.run(event => 'Willkommen in Berlin.');
app.lib.run(event => 'Willkommen in Kreuzberg!', 'kreuzberg');
app.lib.run(event => 'Willkommen in Steglitz!', 'steglitz');

module.exports = app;
```

<br />

**Command (Teletype)**

```ruby
run
```

**Response**

```javascript
'Wilkommen in Berlin!'
```

<br />

**Command (Teletype Studio)**

```ruby
run kreuzberg
```

**Response**

```javascript
'Wilkommen in Kreuzberg!'
```

<br />

**`event` attributes**

- `event.json`: `Object` provides the JSON payload as an object.
- `event.body`: `String` provides the raw json payload.
- `event.type`: `String` will be instantiated to `'run'`.
- `event.action`: `String` bears the action provided by the user or an empty string if no action is provided.
