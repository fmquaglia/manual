The DETA JS library delegates http routing to external frameworks. Consider using [an external framework in your DETA program](/web_frameworks/) such as [Express.js](https://expressjs.com/) or [Koa](https://koajs.com/).

Import the web framework and make calls to the web framework as you would outside of DETA. Then export the app object.

You also can and wrap the external web framework using `detalib.App()`

**Usage Example**

```javascript
const express = require('express');
const app = express();

app.get('/', (req, res) => res.send('Hello from DETA + Express'));

module.exports = app;
```
