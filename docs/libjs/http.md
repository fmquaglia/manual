The DETA JS library delegates http routing to external frameworks. Consider using [an external framework in your DETA program](/web_frameworks/) such as [Express.js](https://expressjs.com/) or [Koa](https://koajs.com/).

Import the web framework and wrap the external web framework using `detalib.App()`. Make calls to the web framework as you would outside of DETA.

Finally export the app object.

**Usage Example**

```javascript
const detalib = require('detalib');
const express = require('express');
const app = detalib.App(express());

app.get('/', (req, res) => {
  res.send('Hello, world.');
});

module.exports = app;
```
