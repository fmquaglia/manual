# DETA Teletype commands (console)

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
The path convention `<group_name>`/`<program_name>` is required if there is a conflict and there is not a groupless named `<program_name>`.

### Changing the Group of a Program

```shell
mv <group_name>/<program_name> <new_group_name>

# mv group_one/prog_one group_two
```
Two programs of the same name cannot live in the same group.

To manipulate groupless programs, the `<group_name>` should be `root`.

```shell
# mv group_two/prog_one root

# mv root/prog_one group_one
```


## Commands Valid After A Program Is 'Open'

### Creating Files

```shell
edit <file_path_and_name>

# edit main.py

# edit utils/calculator.py
```

### Opening Files

```shell
edit <file_path_and_name>

# edit main.py

# edit utils/calculator.py

# edit dir1/dir2/file.py
```

### Mass Deploy

```shell
deploy
```

This command deploys all changes you have made to your files.

### Selected Deploy

```shell
deploy <file_path_and_name_one> <file_path_and_name_two>

# deploy main.py utils/calculator.py
```

Multiple file deploys are accepted, conditional on space separation.

### Removing files

```shell
rm <path_and_file_name_one> <path_and_file_name_two>

# deploy main.py utils/calculator.py
```

Multiple file removals are accepted, conditional on space separation.

### Changing Filename (& Path) In Program

```shell
mv -fl <old_path_name> <new_path_name>

# mv dir1/dir2/file.py main.py
```

### Environment Variables

```shell
env set --<env_var_name> <env_var_val> --<env_var_name2> <env_var_value2>

# env set --my_api_key X2019WzT
```
Environment variable names must start with a letter and can contain letters, digits and `_`. No spaces or other characters are allowed.

### Running Programs

```shell
run --<kwarg_name1> <kwarg_value1> --<kwarg_name2> <kwarg_value2> -<flag1>

# run --name Beverly --age 99 -t
```

### Closing a Program

```shell
close
```

### Package Installation

```shell
pip install <package1_name> <package2_name>

# pip install requests jinja2
```

Multiple packages can be installed, conditional on space separated names.

### Program Specific Information

```shell
meta
```

### vim Keybindings

```shell
vim
```

vim keybindings can be added to the editor.

## Other Commands

### Logout


```shell
logout
```

### CLI Menu

```shell
help
```
