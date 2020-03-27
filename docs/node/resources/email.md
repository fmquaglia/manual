DETA programs have their own unique email address. They can currently send plain text emails (soon they'll also be able to receive email).

To use DETA Email, just import the `email` helper from `detalib`:

```javascript
const { email } = require('detalib');
```

Then use the command below.

**`email(to, subject, message)`** to send an email.

- **`to`** an email address (`String`) or an `Array` of recipients.
- **`subject`** the subject line (`String`).
- **`message`** the email's body (`String`).

##### example code

```javascript
const { app, email } = require('detalib');

app.run(async () => {
  await email('ludwig@example.com', 'Happy Birthday!', 'Dear Ludwig,...');
  await email(
    ['beverly@example.com', 'wesley@example.com'],
    'January Update',
    'Hello team, ..'
  );
});

module.exports = app;
```
