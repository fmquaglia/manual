DETA programs have their own unique email address, from which they can send emails (and soon also receive emails). Only plain text emails can be sent at the moment.

**`email(to, subject, message)`** send an email.

* **`to`**: an email address (`str`) or a `list` of recipients.
* **`subject`** the subject line (`str`).
* **`message`** the email's body (`str`).

##### example code

```python
from deta.lib import app, email

email("ludwig@example.com", "Happy Birthday!", "Dear Ludwig,...")
email(["joe@example.com", "alex@example.com"], "January update", "Hell team, ..")
```
