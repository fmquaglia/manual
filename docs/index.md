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

The output panel on the right hand side of the console should log:

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
import requests

def program(event):
    """The entrypoint to your program logic."""
    url = "https://testapp.deribit.com/api/v2/public/get_index?currency=BTC"
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
    "current_btc_price": 7693.51
}
```

## Using the DETA library (deta.lib)

DETA is bundled with a [library of services](./DETA_lib.md) that power up your programs out of the box. This library includes a schema for accepting outside arguments, database service, a file service, an RPC service for linking multiple DETA programs, a router for turning a DETA program into an API, an HTML rendering service, alongside email and SMS services.


### Storing Data

Let's store our information into a database using the database service so that we can retrieve it later.

Edit your code to import a database from [DETA.lib](./DETA_lib.md) and take a key under which we'll store the price in the database.

```python
from deta.lib import fields, Database
import requests

btc_prices = Database()

class Input(fields.Schema):
    """Please fill out the form."""
    key = fields.Str('Database Key')

def program(event):
    """The entrypoint to your program logic."""
    url = "https://testapp.deribit.com/api/v2/public/get_index?currency=BTC"
    btc_price = requests.get(url).json()['result']['BTC']
    btc_prices.put(event.i.key, btc_price)
    return prices.all()
```

Then `deploy` your changes through the DETA Teletype. 

Upon a successful `changes were deployed` message, run:

```shell
run --key first_price
```
in the Teletype.


Your output should look something like this (but with current information):

```json
{
    "first_price": 7667.19
}
```

## Feedback

Need help, have questions, or want to give feedback?

Please send us a note! hello `@` deta `.` sh