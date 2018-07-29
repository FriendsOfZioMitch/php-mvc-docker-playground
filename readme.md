# ZioMitch's php MVC frameworks playground

Note: this is a work in progress.

This project is aimed to provide a playground for **local development** with various php MVC frameworks.

It provision a common infrastructure to start MVC based projects with a **single click build**, including databases, httpd daemon and the php interpreter.

For any framework will come detailed instructions to import an existing project or create a new project from scratch.

## Clone the project

We are assuming that the host machine is Linux.
We also assume that it comes with Docker and Docker compose installed.

Start cloning the project in your current user home directory folder:

```bash
git clone git@github.com:FriendsOfZioMitch/php-mvc-docker-playground.git
```

## Build Docker

```bash
docker-compose up -d --force-recreate --remove-orphans --build
```

## Hosts file entries

Map the host "framework-gym.local" to point 127.0.0.1 in your hosts file.

## MVC framework project configuration

### Install Laravel

Install a fresh new Laravel project is easy, just launch the following commands:

```bash
mkdir ./app_source; docker-compose run composer composer create-project --prefer-dist laravel/laravel .
```

Reassign write permissions to your current user on the app_source directory:

```bash
sudo chown -R <your_username>:<your_username> app_source
```

Then configure Laravel to to use containerized database settings:

```dotenv
DB_HOST=database
DB_PORT=3306
DB_DATABASE=playground-db
DB_USERNAME=playground-usr
DB_PASSWORD=playground-pwd
```

Check if Laravel is able to access the database:

```bash
docker-compose exec app php artisan tinker
```

And then, once in tinker shell:

```php
DB::connection()->getPdo();
```

If everything is ok, this message should appear:

```text
PDO {#2866
 inTransaction: false,
 attributes: {
   CASE: NATURAL,
   ERRMODE: EXCEPTION,
   AUTOCOMMIT: 1,
   PERSISTENT: false,
   DRIVER_NAME: "mysql",
   SERVER_INFO: "Uptime: 82  Threads: 7  Questions: 8  Slow queries: 0  Opens: 17  Flush tables: 1  Open tables: 11  Queries per second avg: 0.097",
   ORACLE_NULLS: NATURAL,
   CLIENT_VERSION: "mysqlnd 5.0.12-dev - 20150407 - $Id: 38fea24f2847fa7519001be390c98ae0acafe387 $",
   SERVER_VERSION: "5.5.5-10.3.8-MariaDB-1:10.3.8+maria~bionic",
   STATEMENT_CLASS: [
     "PDOStatement",
   ],
   EMULATE_PREPARES: 0,
   CONNECTION_STATUS: "database via TCP/IP",
   DEFAULT_FETCH_MODE: BOTH,
 },
}
```

Check if Laravel home is accessible from http server, pointing your browser to "http://framework-gym.local:8082/".


### Clone an existing Laravel project
If you just want to run an existing laravel project:

```bash
todo
```

# Copyright notes

*Docker is a Copyright © 2018 Docker Inc. All rights reserved.*

*Laravel is a trademark of Taylor Otwell. Copyright © Taylor Otwell.*

*MariaDB is a 2018 Copyright MariaDB Foundation.*

*MySQL is a © 2018 Copyright, Oracle Corporation and/or its affiliates.*

*NGINX is a Copyright © NGINX Inc. All rights reserved.*

