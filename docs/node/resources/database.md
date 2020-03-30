<!-- prettier-ignore-start -->
!!! Note
    Our `detalib` SDK is still work in progress and we will keep improving it in near future.
    If there's a method or feature you'd like, send us an email.
<!-- prettier-ignore-end -->

DETA offers a fully managed key-value store database that's great for storing all kinds of data needed for smaller programs.
There's no limit on the number of databases you create or the amount of data stored.

DETA's Database is built on top of DynamoDB which means it's very reliable and highly scalable. Database is also secure; DETA ensures data and databases can only accessed by the program that created them. We plan to offer database sharing at some point in the future.

## Using Database

### Importing & Instantiating

First import the `Database` class from `detalib`:

```javascript
const { Database } = require('detalib');
```

<br />

With DETA, Databases are created for you automatically when you start using them.
To use a DB, simply "instantiate" it in your code:

##### Code

```javascript
const db = new Database(); // the default DB
const books = new Database('books'); // you can create named DBs
const authors = new Database('authors'); // create as many as you want
```

<br />

### Using the Database

The `Database` instance offers a few useful methods:

#### Put

`db.put(key, value)` inserts a single item into the database. If the key already exists, then the **original value gets overridden**.

* `key`: must be a non-empty string.
    * Examples: `"first"`, `"1"`, `"somerandomid"`
* `value`: can be any objects that can be serialized
    * `String` (_non-empty_)
    * `Number` (_except NaN and Infinity_)
    * `Boolean`
    * Serializable `Object`
    * `null`

##### Code

```javascript
const { app, Database } = require('detalib');
const db = new Database();

app.run(async event => {
  // Valid:
  await db.put('a', 'hello');
  await db.put('b', null);
  await db.put('c', 1213123213);
  await db.put('d', 2);
  await db.put('e', 1.4);
  await db.put('f', 0);
  await db.put('g', False);
  await db.put('h', True);
  await db.put('i', {});
  await db.put('j', [1, 2, 3, 'hello', { nested: [8487637843, 53645] }]);
  await db.put('k', { height: 80 });

  // Not valid:
  // db.put("", "hello") # no empty string as key
  // db.put(1, "hello") # no empty non-string type as key -- use "1" instead
  // db.put("a", "") # no empty string as value -- use None instead
  // db.put("b", NaN) # no NaN as value
});

module.exports = app;
```

<br />

#### Get

`db.get(key)` retrieves an item from the database based on provided key.

Retrieving the item with id `j` from our last example...

##### Code

```javascript
const my_item = await db.get('j');
```

... will come back with following data:

##### Result

```javascript
// value of `my_item`
{
    'key': 'j',
    'data': [
        1,
        2,
        3,
        'hello',
        {
            'nested': [Decimal('8487637843'), Decimal('53645')]
        }
    ]
}
```

Retrieving an item with a key that does not exist will throw an **`Error`**.

<br />

#### Delete

`db.delete(key)` deletes an item from the database based on provided key.

Deleting will not raise any errors, even if the key does not exist.

<br />

#### All

`db.all()` returns a list of all items in the database.
