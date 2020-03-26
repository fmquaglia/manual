Installing and uninstalling packages via pip is currently possible in DETA.

To run a pip command in DETA simply type `pip <pip_command>` into the DETA Studio Teletype after opening a DETA program.

A program's installed packages can be viewed in the "**INFO**" pane under `deps` at the bottom of the DETA console.


## Installing Packages

Multiple packages can be installed by separating their names with a space. 

You can also provide the exact version to be installed -- see the example below.

**Example**
```ruby
pip install requests jinja2==2.11.1
```

If you already have a package installed, you can replace it with a specific version by installing that version.

**Example**
```ruby
pip install requests==2.22.0
```

## Uninstalling Packages

You don't need to specify a version for uninstallation; whatever version of a package is installed will be uninstalled.

**Example**
```ruby
pip uninstall requests jinja2
```


## Cleaning a program

You can uninstall all packages from a program at once by using the `clean` command. 

**Example command**
```ruby
pip clean
```