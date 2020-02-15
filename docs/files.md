!!! Note
    Our `deta.lib` SDK is still work in progress and we will keep improving it in the coming weeks and months.
    If there's a method or feature you _really_ need, send us an email.


Deta Cloud Files is a fully managed file and object storage service that comes handy when storing files in all sizes.

To use DETA Cloud Files just import the `files` helper from `deta.lib`:

```python
from deta.lib import files
```
Then use it

### Put

**`files.put(name, content)`**: store (or update? `fixme`) a text file or binary object.

* **`name`** is the object's name, it must be a string.
*  **`content`** is the object's content, it can be string, bytes or [file object](https://docs.python.org/3.7/library/io.html) **fixme, i need testing`

You can store files in multiple "directories" by prefixing the name of the file with the desired directory name, e.g. `"reports/may.pdf"`.

##### examples
```python
# storing simple text
files.put('cheese.md', "# Deutscher Käse ist...")

# inside a directory
files.put("notes/day14.txt", "We did...")

# storing bytes
files.put('numbers', b"0123456789")

# storing an image
with open("/tmp/photo.png", "rb") as f:
    files.put("photo.png", f)

# storing a text file
with open("/tmp/emails.csv") as f:
    files.put("emails.csv", f)
```

#### Get
If an object is found, it will be streamed back as a `StreamingBody` class, and `None` if there is no object found with the provided key. 

**`files.get(name)`** retrieve a file based on file name or path if it lives inside a directory. `name` is a string

Use the following methods to read your data from **`StreamingBody`**:

**`read(amt=None)`**: Read the data stream. Use `amt` (amount) value to limit the bytes chunks you want to receive at a time (*useful for large files*). Leave it empty if you want to receive all the bytes at once.

**`iter_chunks(chunk_size=1024)`**: Return an iterator to yield chunks of chunk_size bytes from the raw stream.

**`next()`**: Return the next 1k chunk from the raw stream.


**`set_socket_timeout(timeout)`**: Set the timeout seconds on the socket.

**`close()`**: Close the underlying http response stream.

##### code example

```python
text = files.get("hello.txt").read()
files.get("todos/week2/monday.md")
```

### List

for listing all your files or files in a specific directory:

**`files.list(dir=None)`** lists all uploaded files. Provide the directory name to get the files inside it.

##### code examples

```python
 # returns a list of all uploaded files (for the current program)
files.list()

# returns a list of files inside the notes directory
files.list("notes")
files.list("notes/september")
```


### Delete


**`files.delete(name)`** delete a single file from DETA Cloud files.

##### code examples

```python
files.delete("notes.md")
files.delete("notes/september/1.txt")
```