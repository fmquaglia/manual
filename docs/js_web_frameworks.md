DETA is an extremely fast way to get a web framework up and running, supporting most Javascript web frameworks out of the box.

We tested the following frameworks:

- Express

### How to

running a web framework on DETA requires two simple steps.

#### 1) Install the Framework

Open a DETA program and [install the framework dependency](/packages/) using `npm install package` in the [Studio Teletype](/teletype/).

#### 2) Instantiate your web app

Instantinatize your framework and make the necessary method calls within.

#### 3) Export your web app

When the calls to the web framework are all written, then simply export your web app object.

The example below uses Express but the convention is universal.

```javascript
const express = require('express');
const app = express();

app.get('/', (req, res) => res.send('Hello from DETA + Express'));

module.exports = app;
```

<br />

### Using a third-party framework and deta.lib simultaneously

Using detalib alongside a framework in a single DETA program is possible.

To do so, call `App` from `detalib` and instantiate your framework inside it and export the object that you wrapped the framework.

```javascript
const { App } = require('detalib');
const express = require('express');
const app = App(express());

app.get('/', (req, res) => res.send('Hello from DETA + Express'));

app.lib.run('', event => 'Hello from the Teletype');

module.exports = app;
```

### Things to note

- We take care of forwarding HTTP requests to you -- no servers, sockets, or ports to listen to.
- The file system is read-only except /tmp, to which you can write data but it's ephemeral and not consistent across API calls.
