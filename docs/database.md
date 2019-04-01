# Key-Value Store

First import `Database` from `deta.lib`:

```python
from deta.lib import Database
```

One of the benefits of DETA is that you don't need to explicity create a database. You just "ask" for it or in other words "instantiate" it.

Asking for a database:

```python
books = Database()  # DETA will automatically provision a DB for you
```

```python
# instantiate a db
books = Database() # giving a name is optional: Databse('books'). 
# the program's name will be used as name by default.
# you also can re use another database by instantiating 
# it with the program id or provided name: 
users = Database('users')
notes= Database('<id_of_notes_program>')

books.put('mykey', {'my': 'val'})  # value can be: int, str or Decimal
# also lists, dicts that can only contain mentioned types

# the 'books.put' method overides value if key already exists. 
#use 'books.add' to prevent overriding value (will raise KeyError)

# get all books:
books.all()

# get one book
books.get('mykey')

# delete a book
books.delete('mykey')
```
