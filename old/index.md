*These docs are also available at:*

<a href="https://manual.deta.sh/" target="_blank" rel="noreferrer noopener">https://manual.deta.sh/</a>

# Getting Started

Instructions on how to get started with DETA.

## Spaces

Upon logging into DETA your personal space should be activated.

## Creating a Program

Let's get a program created by typing:

```shell
new my_first_program
```

into the [DETA Teletype](./teletype.md). DETA should create and open your program for you.

## Running Your Program

Let's run our new program by entering it into [DETA Teletype](./teletype.md) with arguments
```shell
run --name Beverly --age 34 --likes_ramen true
```
and hitting 'Enter'.

The `CONSOLE` pane on the right hand side of the Studio should log:

```json
{
    "name": "Beverly",
    "age": 34,
    "likes_ramen": true
}
```

## Installing Packages

Let's connect our program to the API-universe by installing the Python 'requests' library by typing the following command into the [DETA Teletype](./teletype.md):

```shell
pip install requests
```

Wait for the requests library to install.

## Editing Programs

Let's edit our program to make an API call using the requests library and return some data. Change the code to:

```python
from deta.lib import app
import requests


@app.run()
def run_handler(event):
    url = "https://test.deribit.com/api/v2/public/get_index?currency=BTC"
    btc_price = requests.get(url).json()['result']['BTC']
    return {
        'current_btc_price': btc_price
    }
```
And then type `deploy` into the DETA Teletype. 

Upon a successful `changes were deployed` message, type `run` into the [DETA Teletype](./teletype.md). 

Your output should look something like this (but with current information):

```json
{
    "current_btc_price": 8693.51
}
```

## Programs as Endpoints

By default in DETA, every program is also an API with a unique URL.

First modify the code to handle GET requests:

```python
from deta.lib import app
import requests

@app.run()
def run_handler(event):
    return price_fetcher()
    
@app.http("/", methods=["GET"])
def get_handler(event):
    return price_fetcher()

def price_fetcher():
    url = "https://test.deribit.com/api/v2/public/get_index?currency=BTC"
    btc_price = requests.get(url).json()['result']['BTC']
    return {
        'current_btc_price': btc_price
    }
```
And then type `deploy` again into the DETA Teletype. 

Go to the `VIEW` pane in the studio, which will make an authenticated GET request to the program's endpoint.

In the URL pane, you will see the program's URL, following the format:

`https://on.deta.dev/<here_is_the_prog_path>`

In this case, hitting the endpoint with a GET request will return json just as running the program from the DETA Teletype did.

```json
{
    "current_btc_price": 8845.89
}
```

The endpoint is private by default, which can be seen by clicking the `INFO` tab and looking at the `API` value, which is `private`.

If you try to open this endpoint in a new browser tab you will get:

```json
{
    "message": "Unauthorized"
}
```

Let's make this endpoint an open endpoint with a command in the DETA Teletype:

```shell
set -api public
```
A few seconds after the `API` value changes to `open`, hitting the URL in a new browser tab should return something like:

```json
{
    "current_btc_price": 8840.99
}
```

Congratulations--you have just created a functional API in DETA!


## Using the DETA library (deta.lib)

DETA is bundled with a [library of services](./DETA_lib.md) that power up your programs out of the box. This library includes a schema for accepting outside arguments, database service, a file service, an RPC service for linking multiple DETA programs, an email service, alongside HTML and JSON response types.


### Storing Data

Let's store our information into a database using the database service so that we can retrieve it later.

Edit your code to import a database from [DETA.lib](./DETA_lib.md) and take a key under which we'll store the price in the database.

```python
from deta.lib import app, fields, Database
import requests

btc_prices = Database()

class Keys(fields.Schema):
    key = fields.Str('Database Key')

@app.run(action="store_price", inp=Keys)
def run_handler(event):
    btc_prices.put(event.i.key, price_fetcher())
    return btc_prices.all()
    
@app.http("/", methods=["GET"])
def get_handler(event):
    return btc_prices.get(event.params.get('key'))

def price_fetcher():
    url = "https://test.deribit.com/api/v2/public/get_index?currency=BTC"
    btc_price = requests.get(url).json()['result']['BTC']
    return str(btc_price)


```

Then `deploy` your changes through the DETA Teletype. 

Upon a successful `changes were deployed` message, run:

```shell
run store_price --key first_price
```
in the Teletype.


The `CONSOLE` pane should look something like this (but with current information):

```json
[
    {
        "key": "first_price",
        "data": "8269"
    },
]
```

The `VIEW` pane should also expose your database to queries by query parameter.

If you hit the endpoint with a request:

`https://on.deta.dev/<prog_path>/?key=first_price`

You should get a response:

```json
{
        "key": "first_price",
        "data": "8269"
}
```

## Feedback

Need help, have questions, or want to give feedback?

Please send us a note! hello `@` deta `.` sh