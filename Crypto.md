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

