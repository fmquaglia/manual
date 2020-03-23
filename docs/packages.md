Installing and uninstalling packages via pip is currently possible in DETA.

To run a pip command in DETA simply type `pip <pip_command>` into the DETA Studio Teletype after opening a DETA program.

A program's installed packages can be viewed in the "**INFO**" pane under `deps` at the bottom of the DETA console.


## Install Packages

Command pattern:

```ruby
pip install <package1_name> <package2_name>
```

Multiple packages can be installed by separating their names with a space. You could also provide the exact version to be installed -- see the example below.

**Example command**
```ruby
pip install requests jinja2==2.11.1
```

## Uninstall Packages

```shell
pip uninstall <package1_name> <package2_name>
```

**Example command**
```ruby
pip uninstall requests jinja2==2.11.1
```
