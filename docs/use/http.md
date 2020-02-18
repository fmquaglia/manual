Using an HTTP endpoint is a great way to connect your program to the outside world.
For example if you want to trigger it from another service (Webhook) or use it as a simple API endpoint.

## URL

Each program gets it's ***unique*** URL, which you can find when you click on the **VIEW** tab on the right of the Studio.:

![Finding the URL of a program](/images/url.png)

The URL looks something like this: **`https://app.deta.sh/abcdefg/`**

## Routing
[Please visit the Router docs](/lib/http.md)

## Authentication

If you copy the URL of freshly created program and paste it into your your browser, you would get this message instead of the expected response: `#!json {"errors":["Unauthorized"]}`.

For now there are 2 convenient ways to authorize HTTP access to your program:

1. Public Access (where you could implement your own auth functionality if needed)
2. API Keys


**You can learn more about these 2 methods [here](sharing.md)**

## Built-in HTTP client and Debugger

[Watch this video](debug.md) for instruction on how to use the built-in HTTP client and real-time debugger.

!!! info
    We're working on OAuth based access. We will let you know when it's been released.