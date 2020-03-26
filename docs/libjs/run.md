**`app.lib.run(action, func)`** is used to execute code following a [run command from Teletype](/use/run). It takes name of the action and the function to be executed.

**Arguments**

- `action`: `String` indicates which **`app.lib.run()`** function to execute.

- `func`: `Function` indicates which function to execute when `action` is passed

<br />

**Usage example:**

```javascript
const detalib = require('detalib');
const app = detalib.App();

app.lib.run('', async event => 'Willkommen in Berlin.');
app.lib.run('kreuzberg', event => 'Willkommen in Kreuzberg!');
app.lib.run('steglitz', event => 'Willkommen in Steglitz!');

module.exports = app;
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

```javascript
'Wilkommen in Berlin!';
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

```javascript
'Wilkommen in Kreuzberg!';
```

<br />

**`event` attributes**

- `event.json`: `Object` provides the JSON payload as an object.
- `event.body`: `String` provides the raw json payload.
- `event.type`: `String` will be instantiated to `'run'`.
- `event.action`: `String` bears the action provided by the user or an empty string if no action is provided.

**Responses**

See [primitive responses](/lib/responses#primitive-responses).
