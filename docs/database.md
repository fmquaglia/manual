!!! Note
    Our `deta.lib` SDK is still work in progress and we will keep improving it in the coming weeks and months.
    If there's a method or feature you _really_ need, send us an email.

DETA offers a fully managed key-value store database for storing all kinds of data needed for smaller programs.
There's no limit on the number of databases you can create or the amount of data stored.
DETA Database is built on top of DynamoDB which means it's very reliable and highly scalable. The databases and the data can only be accessed by the program that created them. We will offer database sharing at some point in the future.

## Using the Database

### Import & instantiate

First import the `Database` class from `deta.lib`:

```python
from deta.lib import Database
```

With DETA, Databases are created for you automatically when you start using them.
To use a DB, simply "instantiate" it in your code:


##### code
```python
db = Database()  # the default DB
books = Database("books")  # you can create named DBs
authors = Database("authors")  # create as many as you want
```

### Using the Database

The `Database` instance offers a couple of useful methods:
#### Put

`db.put(key, value)` Inserts a single item into the database. If the key already exists, then the **original value gets overwritten**.

* `key`: must be a non-empty string. Examples: `"first"`, `"1"`, `"somerandomid"`
* `value`: can be a non-empty `str`, an `int`, a `Decimal` (*no floats, in fact all numbers are stored as `Decimal`*), `boolean`, `None`; `list` and `dict` that contain any of the aforementioned primitive types. Nested lists and dicts are also supported.


##### Code

```python
from deta.lib import app, Database
from decimal import Decimal

db =  Database()

@app.run()
def runner(event):
    # Valid:
    db.put("a", "hello")
    db.put("b", None)
    db.put("c", 1213123213)
    db.put("d", Decimal(2))
    db.put("e", Decimal("1.4"))
    db.put("f", 0)
    db.put("g", False)
    db.put("h", True)
    db.put("i", {})
    db.put("j", [1,2,3, "hello", {"nested": [8487637843,53645]}])
    db.put("k", {"height": Decimal(80)})

    # Not valid:
    # db.put("", "hello") # no empty string as key
    # db.put(1, "hello") # no empty non-string type as key -- use "1" instead
    # db.put("a", "") # no empty string as value -- use None instead
    # db.put("b", 1.4) # no float as value -- use Decimal instead
```

#### Get


`db.get(key)` retrieves an item from the database based on provided key.

Retrieving the item with id `220te3`...
##### Code
```python
my_item = db.get("220te3")
```

... will come back with following data:
##### Result
```python
# value of `my_item`
{
    'key': '220te3',
    'data': [
        Decimal('1'),
        Decimal('2'),
        Decimal('3'),
        'hello',
        {
            'nested': [Decimal('8487637843'), Decimal('53645')]
        }
    ]
}
```

Retrieving an item with a key that does not exist will raise a **`KeyError`** exception.

### Delete

`db.delete(key)` deletes an item from the database based on provided key.

Deleting will not raise any errors, even if the key does not exist.

### All

`db.all()` returns a list of all items in the database.
