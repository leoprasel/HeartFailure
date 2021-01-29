### In this project we will be using Docker, MySQL and python for API handling

#### Docker
In order to create a mysql docker container, we use the following code on the linux command line:

```
docker container run -d -p 3306:3306 --name mysql -e MYSQL_RANDOM_ROOT_PASSWORD=yes mysql
```

Searching the logs for the root password, we get the following key: inus6ciecae8chogahqu3No0iph5ohZo

So now we should structure the SQL database.

```
 CREATE DATABASE cryptoproject;
 use cryṕtoproject;
```
```
 CREATE TABLE IF NOT EXISTS `crypto` (
  `rank_id` int(10) NOT NULL auto_increment,
  `name` varchar(50) NOT NULL,
  `symbol` varchar(10) NOT NULL,
  `price` float(50) NOT NULL,
  `marketcap` float(50) NOT NULL,
  `datetime` DATETIME NOT NULL,
  PRIMARY KEY (`rank_id`)
  );
```

```
from requests import Request, Session
from requests.exceptions import ConnectionError, Timeout, TooManyRedirects
import json
url = 'https://pro-api.coinmarketcap.com/v1/cryptocurrency/listings/latest'
parameters = {
  'start':'1',
  'limit':'2',
  'convert':'USD'
}
headers = {
  'Accepts': 'application/json',
  'X-CMC_PRO_API_KEY': 'be9348e4-68dc-4a62-8b27-91e7698bd09a',
}

session = Session()
session.headers.update(headers)


response = session.get(url, params=parameters)
coins = json.loads(response.text)
#print(json.dumps(data, indent=4, sort_keys=True))

import mysql.connector
def insertTable():
    try:
        connection = mysql.connector.connect(host='localhost')


for coin in coins['data']:
    record = (coin['name'],coin['symbol'],coin['quote']['USD']['price'],coin['quote']['USD']['market_cap'],coin['last_updated'])
```
