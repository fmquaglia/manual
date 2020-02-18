DETA not only focuses on giving you a great experience writing programs,
it also offers you a couple convenient way to interact with them.

## Using Teletype (CLI)

You can find Teletype (our command line interface) in 2 different places:

### 1) Teletype (Studio)

To interact withy our programs in [Teletype (Studio)](https://web.deta.sh/studio), the program needs to be open (`open myprog`).
To invoke the program, use the **command** `run` followed by an optional **action** then followed by the optional **kwargs** and **flags**.

**Command examples**

Invoking the program with no additional arguments:
```ruby
run
```
*This corresponds the with `@app.run()` decorated function. (Notice the lack of action)*

Invoking the program with arguments (but no action).
```ruby
run --name "Jean-Luc Picard" --origin France -likes_earl_gray_tea
```
*The data will be sent as JSON to your program. Flags (prefixed with '`-`') will be set to `true`.*

Invoke the program with and an **action**:

```ruby
run add
```

```ruby
run add --name "Jean-Luc Picard" --origin France -likes_earl_gray_tea
```
*This corresponds the with `@app.run("add")` decorated function. (Notice the "test" action)*


### 2) Teletype (Dash)

Teletype (Dash) offers you an even easier way to call your program. No need to open the program, just use the name of the program instead of the `run` command.

**Command examples**

```ruby
st_captains add --name "Jean-Luc Picard" --origin France -likes_earl_gray_tea
```
etc...
