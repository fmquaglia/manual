**`app.lib.run(func, action='')`** is used to execute code following a [run command from Teletype](/use/run). It takes the function to be executed and the name of the action to trigger the function.

**Arguments**

- `func`: `Function` function to be executed when `action` is passed to the [run command from Teletype](/use/run).

- `action`: `String` name of the action to trigger `func`.

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
'Wilkommen in Berlin!';
```

<br />

**Command (Teletype Studio)**

```ruby
run kreuzberg
```

**Response**

```javascript
'Wilkommen in Kreuzberg!';
```

<br />

**`event` attributes**

- `event.json`: `Object` provides the JSON payload as an object.
- `event.body`: `String` provides the raw JSON payload.
- `event.type`: `String` will be instantiated to `'run'`.
- `event.action`: `String` bears the action provided by the user or an empty string if no action is provided.
