# ZioMitch's php MVC frameworks playground

Note: this is a work in progress.

This project is aimed to provide a playground for **local development** with various php MVC frameworks.

It provision a common infrastructure to start MVC based projects with a **single click build**, including databases, httpd daemon and the php interpreter.

For any framework will come detailed instructions to import an existing project or create a new project from scratch.

# Clone the project

We are assuming that the host machine is Linux.
We also assume that it comes with Docker and Docker compose installed.

Start cloning the project in your current user home directory folder:

```bash
git clone git@github.com:FriendsOfZioMitch/php-mvc-docker-playground.git
```

# Build Docker

```bash
docker-compose up -d --force-recreate --remove-orphans --build
```

## MVC framework project configuration

### Install Laravel

Install a fresh new Laravel project is easy, just launch the following commands:

```bash
rm ./app_source/.gitkeep; docker-compose run composer composer create-project --prefer-dist laravel/laravel .
```

Reassign write permissions to your current user on the app_source directory:

```bash
sudo chown -R you:you app_source
```

Then configure Laravel to to use containerized database settings:

```dotenv
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
todo
```

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

