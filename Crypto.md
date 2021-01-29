### In this project we will be using Docker, MySQL and python for API handling

#### Docker
In order to create a mysql docker container, we use the following code on the linux command line:

```
docker container run -d -p 3306:3306 --name mysql -e MYSQL_RANDOM_ROOT_PASSWORD=yes mysql
```

Searching the logs for the root password, we get the following key: 
