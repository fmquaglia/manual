# DETA Teletype Commands (Studio)

## Conventions
User defined variable inputs are indicated between `<` and `>` symbols, as such: `<variable_name>`. 

Specific examples of valid commands are indicated by `#`.


## Help

```ruby
help
```

## List programs

List all programs:
```ruby
ls
```

Filter by group:
```ruby
ls <group_name>
```

## Create programs

Names can contain letters, digits, `-` and `_`. No spaces or other characters are allowed.

Create a program:
```ruby
new <program_name>
```

Optionally create a program in a group:
```ruby
new <program_name> --group <group_name>
```

## Rename programs

```ruby
mv <program_name> <new_program_name>
```

## Move a program to a different group

```ruby
mv <group_name>/<program_name> <new_group_name>/<new_program_name>
```

## Open programs

A program which does not belong to a group:
```ruby
open <prog_name>
```
A program which belongs to a group:

```ruby
open <group_name>/<program_name>
```
!!! Info
    For program commands `move` and `open`, the `<group_name>/<program_name>` syntax can be shortcut to `<command> <program_name>` if the name is unique across the "Space".

## Run programs

Refer to **[Run docs](use/run.md)** for more details.

## Set environment variables (env vars)

Environment variable names must start with a letter and can contain letters, digits and `_`. No spaces or other characters are allowed.

```ruby
set -envs --<env_var_name> <env_var_val> --<env_var_name2> <env_var_value2>
```

Example
```ruby
set -envs --MY_API_KEY "very secret"
```

## Remove (unset) environment variables (env vars)

```ruby
rm -envs <env_var_name> <env_var_name2> 

```

## Create and edit files

the file will be created if it did not exist.

```ruby
edit <file_name>
```
Directories are not currently supported.


## Deploy (all changed files)

```ruby
deploy
```

## Deploy specific files

```ruby
deploy <file_name_one> <file_name_two>
```

## Delete files

```ruby
rm <file_name_one> <file_name_two>
```

## Rename files

```ruby
mv -fl <old_path_name> <new_path_name>
```
## Close programs

```ruby
close
```

## Cron/Schedules
[Read Cron docs.](use/cron.md)

## Enable public HTTP access 
HTTP is private by default.

```ruby
set -http_auth off
```

## Disable public HTTP access
HTTP is private by default.

```ruby
set -http_auth on
```

The HTTP auth setting can be seen in the `INFO` tab of the Studio, or in the `HTTP Auth` section of a program's settings menu.


##  Enable "Debug Mode"

[Watch this video](debug.md) for more details.

```ruby
set -log debug
```

## Disable "Debug Mode"

```ruby
set -log off
```

## Change DETA Library (`deta.lib`) Version

Usually you don't need to do that manually.

```ruby
set -lib <lib_version>
```

## Toggle VIM keybindings

Vim keybindings can be toggled using the following command.

```ruby
vim
```

## Clear output

Clear Teletype logs

```ruby
clear
```

Clear Teletype output

```ruby
clear -console
```