# Build docker

```bash
docker-compose up -d --force-recreate --remove-orphans --build
```

## MVC framework project configuration

### Install Laravel

Install a fresh new Laravel project is easy, just launch the following commands:

```bash
rm ./app_source/.gitkeep
docker-compose run composer composer create-project --prefer-dist laravel/laravel .
```

Assign write permissions to your current user on the app_source directory:

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
