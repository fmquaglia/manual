Every DETA program has its own HTTP endpoint, which is a great way to connect your program to the outside world.
You can trigger it from another service (i.e. via webhooks) or use it as a simple API endpoint.

## URL

You can a program's ***unique*** URL by clicking on the **VIEW** tab on the right within the [Studio](https://web.deta.sh/studio):

![Finding the URL of a program](/images/url.png)

The URL looks something like this: **`https://app.deta.sh/abcdefg/`**

## Routing
[Please visit the Router docs](/lib/http/)

## Authentication

If you copy the URL of freshly created program and paste it into your your browser, instead of the expected response, you will get this message: `#!json {"errors":["Unauthorized"]}`.

There are 2 ways to authorize HTTP access to your program outside of DETA:

1. Public Access (where you could implement your own auth functionality if needed)
2. API Keys


**You can learn more about these 2 methods [here](/permissions/).**

## Built-in HTTP client and Debugger

[Watch this video](debug.md) for instruction on how to use the built-in HTTP client and real-time debugger.

!!! info
    We're working on OAuth based access. We will let you know when it's been released.
