# LAMP docker-compose Boilerplate

## LARAVEL PERFORMANCE NOTES
If you are going to use Laravel, it will be normally slow a lot in Docker (see: https://dev.to/tylerlwsmith/speed-up-laravel-in-docker-by-moving-vendor-directory-19b9). So you can make these changes to force the "vendor" folder (dependencies folder to be served from the container, not mount from host as normal):
1. Add `- /var/www/html/vendor/` under the `- ./:/var/www/html` line in `docker-compose.yml` (Add a volume to Docker, but exclude "vendor" sub-folder)
2. You need to run `composer install` first at Host (to prepare the "vendor" folder)
3. Each time you run the app, you have to copy "vendor" from Host to Container `docker-compose up -d && docker-compose cp vendor web:/var/www/html/` or just make a `start.sh` file and put that long command into it

## Config your settings before we start
1. Change "yoursite" to anything you like in "docker-compose.yml"
2. Config your site config in /docker/apache/000-default.conf
3. Change mysql root password, first user and password in "docker-compose.yml", and your seed data in "/docker/db/sql/001-yourdb.sql"
4. Change the redis password in "docker-compose.yml"

## Services and default settings

### apache
- Expose port 8000 for http, 444 for https
- You can add many .conf as you want in /docker/apache/
- Included a self signed certificate for https in /docker/apache/ssl, so that it can be used for local development
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
docker-compose exec web bash

docker-compose logs web -f
```
