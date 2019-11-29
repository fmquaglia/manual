# DETA Teletype Commands (Console)

User defined variable inputs are indicated between `<` and `>` symbols, as such: `<variable_name>`. 

Specific examples of valid commands are indicated by `#`.

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

## Program Commands

### Listing Programs
```shell
ls

ls --group <group_name>

# ls --group group_one

ls <group_name>

# ls group_one
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

### Opening a Program

```shell
open <prog_name>

# open prog_one

open <group_name>/<program_name>

# open group_one/prog_one
```
The path convention `<group_name>`/`<program_name>` is required if there is a conflict and there is not a groupless program named `<program_name>`.

### Changing the Group & Name of a Program

```shell
mv <program_name> <new_program_name>

# mv prog_one prog_two

mv <group_name>/<program_name> <new_group_name>/<new_program_name>

# mv group_one/prog_two group_one/prog_two
```
Two programs of the same name cannot live in the same group.

The path convention `<group_name>`/`<program_name>` is required if there is a conflict and there is not a groupless program named `<program_name>`.

To refer to the groupless case, the `<group_name>` should be `root`.

```shell
# mv group_one/prog_two root/prog_one

# mv root/prog_one group_one/prog_one
```

### Scheduling Program Execution

DETA's scheduler accepts cron expressions of length 6, with times in UTC.

```shell
cron <group_name>/<prog_name> <minute> <hour> <monthDay> <weekDay> <year>

# cron group_one/prog_one 0 10 * * ? *
```

Rate based scheduling is also accepted with the `-rate` flag.

```shell
cron <group_name>/<prog_name> -rate <interval> <unit>

# cron group_one/prog_one -rate 3 minutes
```

Rate based scheduling will execute a program every `interval` according to the `unit`. Accepted `unit` values are `minutes`, `hours`, `days`. If the `interval` is `1`, the singular of `minute`, `hour`, or `day` should be used.

### Removing an Execution Schedule for a Program

The execution schedule for a program can be removed with the `-r` flag.

```shell
cron -r <group_name>/<prog_name>

# cron -r group_one/prog_one
```


## Commands Valid After a Program is Open

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


### Mass Deploy

```shell
deploy
```

Deploys all changes you have made to your files.

### Selected Deploy

```shell
deploy <file_name_one> <file_name_two>

# deploy main.py calculator.py
```

Multiple file deploys are accepted, conditional on space separation.

### Removing files

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

### Environment Variables

#### Creation

```shell
env set --<env_var_name> <env_var_val> --<env_var_name2> <env_var_value2>

# env set --my_api_key X2019WzT
```

#### Deletion

```shell
env rm <env_var_name> <env_var_name2> 

# env rm my_api_key
```
Environment variable names must start with a letter and can contain letters, digits and `_`. No spaces or other characters are allowed.

### Running Programs

```shell
run --<kwarg_name1> <kwarg_value1> --<kwarg_name2> <kwarg_value2>

# run --name Beverly --age 99
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

### Execution Schedules

An execution schedule can be set or removed for an open program using the `*this` as an identifier.

```shell
cron *this <minute> <hour> <monthDay> <weekDay> <year>

# cron *this 0/5 8-17 ? * MON-FRI *
```

The `-rate` and `-r` flags can also be used in conjunction with `*this`.

```shell
cron *this -rate <interval> <unit>

# cron *this -rate 10 hours

cron -r *this

# cron -r *this
```

### Program Specific Information

```shell
meta
```

### Vim Keybindings

```shell
vim
```

Vim keybindings can be added to the editor.

### Changing a Program's DETA Library Version

```shell
lib use <lib_version>

# lib use 4
```

### Closing a Program

```shell
close
```

## Other Commands

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
