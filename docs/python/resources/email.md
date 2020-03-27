DETA programs have their own unique email address. They can currently send plain text emails (soon they'll also be able to receive email).

To use DETA Email, just import the `email` helper from `deta.lib`:

```python
from deta.lib import email
```
Then use the command below.

**`email(to, subject, message)`** to send an email.

* **`to`** an email address (`str`) or a `list` of recipients.
* **`subject`** the subject line (`str`).
* **`message`** the email's body (`str`).

##### example code

```python
from deta.lib import app, email

email("ludwig@example.com", "Happy Birthday!", "Dear Ludwig,...")
email(["beverly@example.com", "wesley@example.com"], "January Update", "Hello team, ..")
```
