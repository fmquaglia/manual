Installing packages via pip is currently possible in DETA.

However, the DETA package manager is under heavy development and performance has room for improvement. Some Packages with **C** dependencies might fail. If that happens, **please [contact us](contact.md)** to patch our installer.

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
