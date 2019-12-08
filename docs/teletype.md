# DETA Teletype Commands (Console)

## Conventions
User defined variable inputs are indicated between `<` and `>` symbols, as such: `<variable_name>`. 

Specific examples of valid commands are indicated by `#`.

Teletype commands on DETA programs follow the convention:

`<action> <group_name>/<program_name> <[action specific args]>` 

`<group_name>/<program_name>` can be shortcut to `<program_name>` if there is no conflict or to refer to a groupless program of `<program_name>`.

`<group_name>/<program_name>` can be omitted if a program is open in the console and the action applies to said open program.

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

### Running Programs

```shell
run <group_name>/<program_name> --<kwarg_name1> <kwarg_value1> --<kwarg_name2> <kwarg_value2>

# run <group_name>/<program_name> --name Beverly --age 99

# run --name Beverly --age 99
```

After a program is opened the path can be dropped to run it as a shortcut.

### Opening a Program

```shell
open <prog_name>

# open prog_one

open <group_name>/<program_name>

# open <group_name>/<program_name>
```

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

## Space Commands

### Listing Spaces
```shell
ls -s
```

### Creating a Space
```shell
new -s <space_name>

# new -s space_one
```

### Opening a Space

```shell
open -s <space_name>

# open -s space_one
```

## Commands for Program-Specific Objects

Many objects are sub-resources belonging under DETA *programs*. The conventions for this case are either of:

```shell
<action> <program_path> -<object_flag> <[flag specific args]>

<action> -<object_flag> <program_path> <[flag specific args]>
```

When a program is open in the console, the path can be dropped as a shortcut.

### Execution Schedules

DETA's scheduler accepts cron expressions of length 6, with times in UTC.

#### Setting:
```shell
set <group_name>/<prog_name> -cron <minute> <hour> <month_day> <week_day> <year>

# set group_one/prog_one -cron 0 10 * * ? *
```

Rate based scheduling is also accepted:

```shell
set <group_name>/<prog_name> -cron <interval> <unit>

# set group_one/prog_one -cron 3 minutes
```

Rate based scheduling will execute a program every `interval` according to the `unit`. 

Accepted `unit` values are `minutes`, `hours`, `days`. 

If the `interval` is `1`, the singular of `minute`, `hour`, or `day` should be used.

#### Removing:

```shell

rm <group_name>/<prog_name> -cron 

# rm group_one/prog_one -cron 
```

The program path can be dropped to set or remove schedules for open programs.

### APIs

#### Public

```shell
set <group_name>/<prog_name> -api public

# set group_one/prog_one -api public
```

#### Private (default setting)

```shell
set <group_name>/<prog_name> -api private

# set group_one/prog_one -api private
```

The program path can be dropped for open programs to make it's API public or private.

### Program Specific Permissions

```shell
set <group_name>/<prog_name> -perms --username_one '<[perms]>' --username_two '<[perms]>'

# set group_one/prog_one -perms --beverly 'edit, run' --wesley 'run'

# set -perms DETA -all
```
As a *Space admin* or creator of a program, you can set user level permissions of a program.

Accepted permissions are `edit`, `run`, and `full`.

Permissions should be encapsulated in single quotes and comma separated.

The program path can be dropped for open programs.

## Commands Valid After a Program is Open

Files, packages, environment variables, and the DETA lib version can only be manipulated in the console in the context of an open program.

### Creating Files

```shell
edit <file_name>

# edit main.py

# edit post.md
```

Directories are not currently supported.

### Opening Files

```shell
edit <file_name>

# edit main.py
```


### Mass Deploy (all changed files)

```shell
deploy
```

### Selected Deploy

```shell
deploy <file_name_one> <file_name_two>

# deploy main.py calculator.py
```

Multiple file deploys are accepted, conditional on space separation.

### Removing Files

```shell
rm <file_name_one> <file_name_two>

# rm main.py calculator.py
```

Multiple file removals are accepted, conditional on space separation.

### Changing Filenames

```shell
mv -fl <old_path_name> <new_path_name>

# mv file.py calculator.py
```

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

### Environment Variables

#### Setting:

```shell
set -env --<env_var_name> <env_var_val> --<env_var_name2> <env_var_value2>

# set -env --my_api_key X2019WzT
```

#### Removing:

```shell
rm -env <env_var_name> <env_var_name2> 

# rm -env my_api_key
```
Environment variable names must start with a letter and can contain letters, digits and `_`. No spaces or other characters are allowed.


### Changing a Program's DETA Library Version

```shell
set -lib <lib_version>

# set -lib 10
```

### Program Specific Information

```shell
meta
```

### Closing a Program

```shell
close
```

## Other Commands

### Keybindings

```shell
set -bindings vim

set -bindings emacs
```

Vim and emacs keybindings can be added to and removed from the editor.

```shell
rm -bindings
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
