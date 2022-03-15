# lamp-docker-compose-boilerplate

## Before we start
1. Change "yoursite" to anything you like in "docker-compose.yml"
2. Config your site config in /docker/apache/000-default.conf
3. Change mysql root password, first user and password in "docker-compose.yml", and your seed data in "/docker/db/sql/001-yourdb.sql"
4. Change the redis password in "docker-compose.yml"

## Services and default settings

### apache
- Expose port 8000 for http, 444 for https
- You can add many .conf as you want in /docker/apache/
- Include self signed certificate for https in /docker/apache/ssl, so that it can be used for local development
- You can see logs in /docker/apache/logs

### php
- You can change the version of php by tags (See supported tags here: https://hub.docker.com/_/php)
- You can config your php.ini in /docker/php/php.ini
- Default timezone is Asia/Tokyo

### composer
- You can use composer to install your project dependencies after build and run the containers, then
```
docker-compose exec web bash
```

### mysql
- You can change the version of mysql by tags (See supported tags here: https://hub.docker.com/_/mysql)
- You can have seed data at the beginning in /docker/db/sql/ folder (it also be .sql or .sh) and run by order
- You can config mysql.cnf in /docker/db/mysql.cnf
- Default timezone is Asia/Tokyo
  
### redis
### phpmyadmin

## Usage
```
docker-compose up -d
```

## Usefull commands
```
docker-compose exec yoursite-web bash

docker-compose logs yoursite-web -f
```