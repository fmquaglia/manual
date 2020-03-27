* We support Python 3.7 and Node.js 12.x code for now.
* Every program you use gets it's own sandboxed Linux VM. Nobody can access your code and VM but you.
* You are suppose to interact with the filesystem, it's not a security vulnerability.
* Each program has a key and secret keys set in the environment, these are specific to your program and not the DETA system. Make sure to not share them to keep your own data safe.
* An execution timeouts after 10s. Contact us for increase (up to 15 minutes/execution).
* 128 MB of RAM for *each* execution. Contact us for increase (up to 3 GB/execution).
* Read-only file system. **Only `/tmp` can be written to**. It has a 512 MB storage limit.
* Invocations have an execution processes/threads of 1024.
* HTTP Payload size limit is 5.5 MB.
* Emails are limited to 100 a day.

More coming soon.