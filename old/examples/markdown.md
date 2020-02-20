# Markdown Rendering
## Configuration
### Required Files
`main.py`
<br/>
`post.md`

To create `post.md`, enter:
```shell
edit post.md
```
### Dependencies
`markdown`

To install `markdown`, enter:
```shell
pip install markdown
```

## main.py

```python
from deta.lib.responses import HTML
from markdown import markdown

def program(event):
    post = markdown(open("post.md").read())
    return HTML(post)
```

## post.md

```md
Here is a paragraph

<br/>
Here is code
    
    def func(x):
        return x*x
```

## Viewing
To deploy changes, type `deploy` in the DETA Teletype.

To view changes, click the `GET` view in the navbar while the program is open. The `GET` view will auto update each time you `deploy` changes.

<br/>

# Adding Dynamic Data with requests & jinja2

To add dynamically updating data via an API call, install the `requests` and `jinja2` libraries.

```shell
pip install requests jinja2
```

## main.py

```python
from deta.lib.responses import HTML
from markdown import markdown
import requests
from jinja2 import Template

def program(event):
    url = "https://test.deribit.com/api/v2/public/get_index?currency=BTC"
    btc_price = btc_price = requests.get(url).json()['result']['BTC']
    post_template = Template(markdown(open("post.md").read()))
    return HTML(post_template.render(data=btc_price))
```

## post.md

```md
# Header


Here is a paragraph

<br/>
Here is code
    
    def func(x):
        return x*x

<br/>
Here is the bitcoin price:
<p> ${{ data }} </p>
```

Each time the url is hit, the current bitcoin price should be inserted in the page.