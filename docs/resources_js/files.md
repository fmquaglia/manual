!!! Note
DETA Library `detalib` is still work in progress and we will keep improving it in the coming weeks and months.
If there's a method or feature you _really_ need, send us an email.

Deta Cloud Files is a fully managed file and object storage service that comes in handy when storing files of all sizes.

To use DETA Cloud Files just import the `files` helper from `detalib`:

```javascript
const { files } = require('detalib');
```

Then use one of the following four methods below.

### Put

**`files.put(name, content)`**: store a text file or binary object.

- **`name`** is the object's name, it must be a string.
- **`content`** is the object's content. It can be one of the following:

  - `String`
  - `Buffer`
  - `Blob`
  - `Typed Array`
  - `ReadableStream`

You can store files in multiple "directories" by prefixing the name of the file with the desired directory name, e.g. `"reports/may.pdf"`.

##### Code Examples

```javascript
// storing simple text
await files.put('cheese.md', '# Deutscher Käse ist...');

// inside a directory
await files.put('notes/day14.txt', 'We did...');

// Will come up with more examples during test.
```

<br />

### Get

**`files.get(name)`** retrieves a file based on file name or path if it lives inside a directory.

- **`name`** string
- return value:
  - a `Buffer` will be sent back if an object is found with the provided `name`.
  - _**Need to see what happens when the object with the name**_

##### Code Example

```javascript
const buf = await files.get('todos/week2/monday.md');
const markdown = buf.toString('utf8');
```

See the Node.js documentation to read your data from a **`Buffer`**

##### Code Example

```javascript
text = files.get('hello.txt').read();
```

<br />

### List

for listing all your files or files in a specific directory:

**`files.list(dir=None)`** lists all uploaded files. Provide the directory name to get the files inside it.

##### Code Examples

```python
 # returns a list of all uploaded files (for the current program)
files.list()

# returns a list of files inside the notes directory
files.list("notes")
files.list("notes/september")
```

<br />

### Delete

**`files.delete(name)`** delete a single file from DETA Cloud files.

##### Code Examples

```python
files.delete("notes.md")
files.delete("notes/september/1.txt")
```
