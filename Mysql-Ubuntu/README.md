#docker-ubuntu-mysql
Dedicated mysql container, intended for exposure to another container.
 
## About

This mysql container is based on ubuntu:20.04, and has the following in addition:

* mysql-server
* Listens on 0.0.0.0 instead of the default 127.0.0.1
* Port 3306 is exposed, in case you are not linking containers
* Allows for a root password to be set when run for the first time

## Example

### Building docker image
```shell
docker build -t mysql:1.0 .
```


### Running

Simple, not exposed:

```shell
docker run -d --name="mysql-run" \
    -e "MYSQL_PASSWORD=password" \
    mysql:1.0
```

Exposed: 

```shell
docker run -d --name="mysql-run" \
    -e "MYSQL_PASSWORD=password" \
    -p 3306:3306 \
    mysql:1.0
```
With Volume:
```shell
docker run -d -p 3306:3306 \
    --name="mysql-run" \
    -e "MYSQL_PASSWORD=password" \
    -v ~/mysql/data:/home/mysql \
    mysql:1.0
```
docker exec -it mysql-run /bin/bash
mysql -p -e "SHOW DATABASES;"

Note: 
- -v ~/mysql/data:/home/mysql \
