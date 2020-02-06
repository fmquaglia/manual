# DETA Teletype Commands (Studio)

## Conventions
User defined variable inputs are indicated between `<` and `>` symbols, as such: `<variable_name>`. 

Specific examples of valid commands are indicated by `#`.


## Program Commands

### Listing Programs

All programs in a space
```shell
ls
```

Filter by group
```shell
ls <group_name>

# ls group_one

ls --group <group_name>

# ls --group group_one
```


### Creating a Program

```shell
new <program_name>

# new prog_one

new <program_name> --group <group_name>

# new prog_one --group group_one
```
Names can contain letters, digits, `-` and `_`. No spaces or other characters are allowed.

If the `--group` keyword is not specified, the program will be groupless.


### Changing the Group & Name of a Program

```shell
mv <program_name> <new_program_name>

# mv prog_one prog_two

mv <group_name>/<program_name> <new_group_name>/<new_program_name>

# mv group_one/prog_two group_one/prog_two
```

To refer to the groupless case, the `<group_name>` should be `root`.

```shell
# mv group_one/prog_two root/prog_one

# mv root/prog_one group_one/prog_one
```

Two programs of the same name cannot live in the same group.

### Opening a Program

```shell
open <prog_name>

# open prog_one

open <group_name>/<program_name>

# open <group_name>/<program_name>
```
<br/>

For program commands `move` and `open`, `<group_name>/<program_name>` can be shortcut to `<program_name>` if there is no conflict or to refer to a groupless program of `<program_name>`.

## Commands Valid After a Program is Open

### Running Programs

```shell
run <action> --<kwarg_name1> <kwarg_value1> --<kwarg_name2> <kwarg_value2>

# run --name Beverly --age 99

# run database_write --name Beverly --age 99
```

An action is optional argument which provides granular control over which block of code in `main.py` will run on command. By default when the `<action>` variable is ommited, the `app.run()` function in `main.py` will run.

### Files


#### Creating Files

```shell
edit <file_name>

# edit main.py

# edit post.md
```

Directories are not currently supported.

#### Opening

```shell
edit <file_name>

# edit main.py
```


#### Mass Deploy (all changed files)

```shell
deploy
```

#### Selected Deploy

```shell
deploy <file_name_one> <file_name_two>

# deploy main.py calculator.py
```

Multiple file deploys are accepted, conditional on space separation.

#### Removing

```shell
rm <file_name_one> <file_name_two>

# rm main.py calculator.py
```

Multiple file removals are accepted, conditional on space separation.

#### Changing Filenames

```shell
mv -fl <old_path_name> <new_path_name>

# mv -fl file.py calculator.py
```

### Program Specific Information

```shell
meta
```

### Closing a Program

```shell
close
```

## Commands for Other Program-Specific Settings

Many settings belonging under DETA *programs*. The conventions for this case are:

```shell
<set || rm> -<object_flag> <[flag specific args]>
```

These commands also require a program be open.

### Execution Schedules

DETA's scheduler accepts cron expressions of length 6, with times in UTC.

#### Setting:
```shell
set -cron <minute> <hour> <month_day> <week_day> <year>

# set -cron 0 10 * * ? *
```

Rate based scheduling is also accepted:

```shell
set -cron <interval> <unit>

# set -cron 3 minutes
```

Rate based scheduling will execute a program every `interval` according to the `unit`. 

Accepted `unit` values are `minutes`, `hours`, `days`. 

If the `interval` is `1`, the singular of `minute`, `hour`, or `day` should be used.

#### Removing:

```shell

rm -cron 
```

### HTTP routes

#### Public

```shell
set -http_auth off
```

#### Private (default setting)

```shell
set -http_auth on
```

The HTTP auth setting can be seen in the `INFO` tab of the Studio, or in the `HTTP Auth` section of a program's settings menu.

### Program Specific Permissions

#### Setting

```shell
set -perms --<username_one> <access_level> --<username_two> <access_level>

# set -perms --beverly view --wesley run

# set -perms --deta -full
```
As a *Space admin* or creator of a program, you can set user level permissions of a program.

Accepted permissions are `view`, `run`, or `full`.

#### Removing

```shell
rm -perms --<username_one> <access_level> --<username_two> <access_level>

# rm -perms --beverly view --wesley run
```

#### Listing

```shell
ls -perms

# ls -perms
```
A program's permission levels can be listed.

### Log Levels

A log level will cache information from incoming requests to a program, allowing this information to be easily seen, edited and replayed.

####  Setting

```shell
set -log debug

set -log off
```

Current log levels are `debug` and `off`.

A log-level of `debug` will cache incoming request types, payloads, and headers, which can be edited and replayed from the `CONSOLE` view of the `Studio`.

#### Removing

```shell
rm -log
```

Removing the log-level of a program is equivalent to setting it to `off`, caching no incoming data.

### Environment Variables

#### Setting:

```shell
set -envs --<env_var_name> <env_var_val> --<env_var_name2> <env_var_value2>

# set -envs --my_api_key X2019WzT
```

#### Removing:

```shell
rm -envs <env_var_name> <env_var_name2> 

# rm -envs my_api_key
```
Environment variable names must start with a letter and can contain letters, digits and `_`. No spaces or other characters are allowed.


### Changing a Program's DETA Library Version

```shell
set -lib <lib_version>

# set -lib 10
```

## Other Commands

### Package Installation

```shell
pip install <package1_name> <package2_name>

# pip install requests jinja2 ffmpeg markdown
```

Multiple packages can be installed, conditional on space separation.

### Package Uninstallation

```shell
pip uninstall <package1_name> <package2_name>

# pip uninstall requests jinja2
```

Multiple packages can be uninstalled, conditional on space separation.

### Package Cleaning

```shell
pip clean
```

All packages can be removed with the clean command.

### Keybindings

```shell
vim
```

Vim keybindings can be added to and removed from the editor.

```shell
vim
```

### Logout


```shell
logout
```

### CLI Menu

```shell
help
```


## Feedback

Need help, have questions, or want to give feedback?

Please send us a note! hello `@` deta `.` sh
