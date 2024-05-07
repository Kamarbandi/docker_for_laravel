To download laravel, run the following command (laravel will load into the src folder, http://localhost:8000)

```sh
docker-compose run composer create-project laravel/laravel .
```

To bring up the required containers, run the command below and start working in your laravel project
```sh
docker-compose up nginx -d
```

To run php artisan, run the following command (I created my own container for artisan, it is easy to use)
```sh
docker-compose run artisan migrate

docker-compose run artisan list
```

> after download laravel do not forget change .env file
```sh
DB_CONNECTION=sqlite
DB_HOST=mysql
DB_PORT=3306
DB_DATABASE=laravel_db
DB_USERNAME=laravel
DB_PASSWORD=password
```


> Note: `Docker: The stream or file "/var/www/html/storage/logs/laravel.log" could not be opened: failed to open stream: Permission denied`

## causes and solution

- The storage link isn't properly set, you can read about it  [here](https://laravel.com/docs/11.x/filesystem#the-public-disk), after launching app container, you should do php artisan storage:link to check whether proper link is there.
in our case like so: docker-compose run artisan storage:link
- You don't have the proper right for the given folder, from default, logs folder should have www-data writable rights.
Just add the proper rights by: chown -R www-data:www-data * (in our case: go inside of php container and run this command: chown -R www-data:www-data *)