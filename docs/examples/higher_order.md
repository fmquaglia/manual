# Higher Order DETA Programs

Here is an example of implementing a map using multiple DETA programs, to illustrate how they can be used in a higher order fashion.

The example is made of:

* a map program (*mapper*) that takes:
    * `func` of type `Str`: another DETA program's id (one of two callee programs)
    * `arr` of type `Str`: a serialized array of integers

* two callee programs (*square* and *doubler*) that each take:
    * `arg` of type `Int`: an integer

* an executor program (*executor*) that takes:
    * `execute` of type `Str`: specifies which program to call 

The mapper program applies the callee program `func` to each element `arg` in the array `arr`, returning the mapped version.

The executor program coordinates the process for the user, displaying the result.

This example requires copying the `prog_id` of a specific callee function to the `load` module of the [DETA library](../DETA_lib.md), indicated between brackers `<prog_id_of_callee>`.

## mapper
### main.py
```python
from deta.lib import fields, load
import json

class Input(fields.Schema):
    func = fields.Str('func')
    arr = fields.Str('array')

def program(event):
    func = load(event.i.func)
    lst = [func(arg=i) for i in json.loads(event.i.arr)]
    return lst
```

## Callee 1, (doubler)
### main.py
```python
from deta.lib import fields

class Input(fields.Schema):
    arg = fields.Int('arg')
    
def program(event):
    return event.i.arg*2
```

## Callee 2, (square)
### main.py
```python
from deta.lib import fields

class Input(fields.Schema):
    arg = fields.Int('arg')
    
def program(event):
    return event.i.arg**2
```

## executor
### main.py
```python
from deta.lib import fields, load
import json

mapper = load(<prog_id_of_mapper>)

class Input(fields.Schema):
    execute = fields.Str('execute')

def program(event):
    """The entrypoint to your program logic."""
    doubler = <prog_id_of_doubler>
    square = <prog_id_of_square>
    func = doubler
    if event.i.execute == "square":
        func = square
    arr = [1, 2, 3, 4, 5]
    return mapper(func=func, arr=json.dumps(arr))
```

## Running the program
```shell
open executor

run
```

response:
```json
[
    2,
    4,
    6,
    8,
    10
]
```

response:
```shell
run --execute square
```

```json
[
    1,
    4,
    9,
    16,
    25
]
```