# Installing packages

Installing simple packages via pip is currently possible but might not work for packages with C dependencies.

Most packages with C dependencies will fail! (any ML, OCR stuff, ...)

Syntax:

```bash
pip install mypackage
```

!!! attention
    After trying to install a a package, Deta is not able to identify if the install was successful or not, pip does provide easy programmatic way to find that out.

Please read the output and check for errors. If you found a critical error, please run: `pip remove mypackages` to remove it from the DB.

!!! note
    Some errors are not critical and the package will be installed anyway, it's worth trying the package first in your program before removing it.

## To list your installed packages

```bash
pip list
```