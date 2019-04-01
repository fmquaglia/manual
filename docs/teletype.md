# Teletype commands (console)

## List your programs

```bash
ls
```

## Create a program
Names can contain letters, digits, `-` and `_`. No spaces or other characters are allowed.

```
new <name>
```

## Running your program

You can run your program from the Teletype using the `run` keyword.

```bash
run <kwargs>
run -name max -age 66 
```

## Update your code/deploy

```bash
deploy
```

## Open another program

```bash
open <name>
```

## close a program

```bash
close
```

## Create cron/schedule

This feature is not reliable and will be re-written very soon.
I suggest not using it.

```bash
repeat -r <number> -u  <minute|minutes|hour|hours|day|days>
```

## Logout from your deta session

```bash
logout
```

## Meta info

Get meta info about a program (mostly for my debugging)

```bash
meta
```
## dash

Open the dashboard.

```bash
dash
```
