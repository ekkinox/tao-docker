# Docker set up for TAO

Ready to use docker set up for working with [package-tao](https://github.com/oat-sa/package-tao).
- Php-fpm 7.1
- Nginx
- MariaDB

## Set up

In your `package-tao` installation root folder, copy provided:
- docker folder
- docker-compose.yml file


## Usage

Up the docker stack:

```
$ docker-compose up -d
```

You can then access:
- TAO on `http://localhost` on port 80
- the database on `localhost` on port 3306

Extra: If needed, this is the CLI needed to install TAO using this docker stack:
```
docker exec -it <FPM-CONTAINER-ID> php tao/scripts/taoInstall.php \
    --db_driver pdo_mysql \
    --db_host tao_mariadb \
    --db_name tao \
    --db_user tao \
    --db_pass tao \
    --module_namespace http://sample/first.rdf \
    --module_url http://localhost \
    --user_login admin \
    --user_pass admin \
    -e taoCe
```

## Running tests from container

This stack also permit to run integration / functional tests of TAO.

For this , you need to set up TAO config as follow:

```
# package-tao/config/generis.conf.php
...
# paths
define('ROOT_PATH','/var/www/html/');
define('ROOT_URL','http://tao_nginx/');
...
```

And then run tests:
```
docker exec -it <FPM-CONTAINER-ID> vendor/bin/phpunit anyTest
```




