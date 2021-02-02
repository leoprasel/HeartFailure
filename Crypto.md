### In this project we will be using Docker, MySQL and python for API handling
#### We'll extract data from CoinMarketCap, a cryptocurrency website that shows the current price of all the different coins.
#### After extracting it using it's API with python, we'll store the data in a MySQL database with the help of Docker. 

#### Docker and Docker Container
In order to create a mysql docker container, we use a docker container with the following configuration:

```
version: "3.3"

services:
  mysql:
    image: mysql:5.7
    ports:
      - "3306:3306"
    volumes:
      - /home/leo/cryptoproject/database:/var/lib/mysql
    environment:
      - MYSQL_ROOT_PASSWORD=password
      - MYSQL_DATABASE=crypto
      - MYSQL_USER=user
      - MYSQL_PASSWORD=password
```

So now we should structure and create the SQL table.

```
 docker exec -it cryptoproject_mysql_1
 use cryṕto;
```

#### mySQL

```
 CREATE TABLE IF NOT EXISTS `crypto` (
  `rank_id` int(10) NOT NULL auto_increment,
  `name` varchar(50) NOT NULL,
  `symbol` varchar(10) NOT NULL,
  `price` float(50) NOT NULL,
  `marketcap` float(50) NOT NULL,
  `datetime` varchar(50) NOT NULL,
  PRIMARY KEY (`rank_id`)
  );
```
Now finally, we can get some data using an API with the help of python, and inserting this into the mySQL database server.

#### python
```
from requests import Request, Session
from requests.exceptions import ConnectionError, Timeout, TooManyRedirects
import json
import mysql.connector

#SQL database configs
config = {
  'host': 'localhost',
  'port': 3306,
  'user': 'user',
  'password': 'password',
  'database': 'crypto'
}

cnx = mysql.connector.connect(**config)
cursor = cnx.cursor()
sql = "INSERT INTO crypto (name, symbol, price, marketcap, datetime) VALUES (%s,%s,%s,%s,%s)"


#API data import
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

for coin in coins['data']:
    record = (coin['name'],coin['symbol'],coin['quote']['USD']['price'],coin['quote']['USD']['market_cap'],coin['last_updated'])
    cursor.execute(sql,record)
    cnx.commit()

print(cursor.rowcount, 'records inserted.')
```
Testing our results...\
\
mysql> SELECT * FROM crypto;\
+---------+----------+--------+--------------------+--------------------+--------------------------+\
|&nbsp;rank_id&nbsp;|&nbsp;name&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;|&nbsp;symbol&nbsp;|&nbsp;price&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;|&nbsp;marketcap&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;|&nbsp;datetime&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;|\
+---------+----------+--------+--------------------+--------------------+--------------------------+\
|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;1&nbsp;|&nbsp;Bitcoin&nbsp;&nbsp;|&nbsp;BTC&nbsp;&nbsp;&nbsp;&nbsp;|&nbsp;&nbsp;33616.63914384671&nbsp;|&nbsp;&nbsp;625829810216.7985&nbsp;|&nbsp;2021-02-02T01:56:02.000Z&nbsp;|\
|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;2&nbsp;|&nbsp;Ethereum&nbsp;|&nbsp;ETH&nbsp;&nbsp;&nbsp;&nbsp;|&nbsp;1375.0092892043913&nbsp;|&nbsp;157435816086.15372&nbsp;|&nbsp;2021-02-02T01:56:02.000Z&nbsp;|\
+---------+----------+--------+--------------------+--------------------+--------------------------+\

### Success! We did it!


