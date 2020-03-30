DETA Node.js runtime delegates HTTP routing to external frameworks. Consider using [an external framework in your DETA program](/web_frameworks/) such as [Express.js](https://expressjs.com/) or [Koa](https://koajs.com/).

Import the web framework and make calls to the web framework as you would outside of DETA. Then export the app object.

**Express Usage Example**

```javascript
const express = require('express');
const app = express();

app.get('/', (req, res) => res.send('Hello from DETA + Express'));

module.exports = app;
```

**Koa Usage Example**

```javascript
const Koa = require('koa');
const app = new Koa();

app.use(async ctx => {
  ctx.body = 'Hello from DETA + Koa';
})

module.exports = app;
```