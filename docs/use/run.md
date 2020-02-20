DETA not only focuses on giving you a great experience writing programs,
it also offers you a couple convenient ways to interact with them.

## Using Teletype

You can find Teletype (DETA's command line interface) in 2 different places:

### 1) Teletype (Studio)

In the studio, where you can edit programs, the Teletype lets you quickly navigate, edit, and run your programs. A list of Studio Teletype commands is [here](../../teletype/).

To run the program, use the **command** `run` followed by an **action** (optional) then followed by **kwargs** and **flags** (both optional).

```ruby
run <action> -<flag_one> --<kwarg_one> <kwarg_val_one>
```
*To run our programs in the [Teletype (Studio)](https://web.deta.sh/studio), the program needs to be open (`open myprog`) and you need to have a ['full' access permission](../../permissions/).*

<br />

**Command examples**

Running the program:
```ruby
run
```
*This corresponds the with [`@app.run()`](/lib/run/) decorated function. (Notice the lack of action)*

<br />

Running the program with an **action**:

```ruby
run add
```
*This corresponds the with [`@app.run("add")`](/lib/run/) decorated function. (Notice the "add" action)*

<br />

Running the program with arguments (but no **action**):
```ruby
run --name "Jean-Luc Picard" --origin France -likes_earl_gray_tea
```
*The data will be sent as JSON to your program. Flags (prefixed with `-`) will be set to `true`.*

<br />

Running the program with an **action** and arguments:
```ruby
run add --name "Jean-Luc Picard" --origin France -likes_earl_gray_tea
```

<br />

### 2) Teletype (Dash)

The Dashboard's Teletype let's you run program without needing to `open` it. Just use the name of the program instead of the `run` command.

```ruby
<prog_name> <action> -<flag_one> --<kwarg_one> <kwarg_val_one>
```

*The Teletype (Dash) lets you run programs where you have a ['run' or 'full' access permission](/permissions/).*

<br />

**Command examples**

```ruby
st_captains add --name "Jean-Luc Picard" --origin France -likes_earl_gray_tea
```
