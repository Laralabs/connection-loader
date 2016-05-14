# Connection Loader for Laravel 5

Have you ever wanted to add database connections from the backend of a Laravel application without the need to edit the configuration files?

Connection Loader for Laravel is a ServiceProvider that loads database connection details from a table in the specified database connection.

You can then access these connections using their name property's with conventional Laravel techniques.

## Installation

Install via composer by adding the following line to your `composer.json` file:

```php
"laralabs/connection-loader": "~1.0.7"
```

After updating composer you will need to add the ServiceProvider to the providers array in `config/app.php`

```php
Laralabs\ConnectionLoader\ConnectionLoaderServiceProvider::class,
```

Once you have added this line to your applications configuration file run the following command the publish the config file to `config/connectionloader.php` and migration file to `database/migrations/2016_05_02_000000_create_connection_loader_table.php`:

```php
php artisan vendor:publish
```

You should receive confirmation that the files have been copied over from artisan.

Now the database table needs to be created, run the database migration with (this will run using the default connection and with a table name of connection_loader):

```php
php artisan migrate
```

Once the database table has been created the configuration file located at `config/connectionloader.php` needs to be altered, here are it's default values:

```php
<?php

return array(
    'enabled'       =>  false,
    'connection'    =>  'mysql',
    'table'         =>  'connection_loader',
    'check_enabled' =>  false,
);
```
Set the value of `connection` to your default connection, default Laravel value provided.

If you altered the connection or database table in the migration before running `php artisan migrate` then you will need to update the configuration file to reflect the changes before enabling Connection Loader.

Set the value of `enabled` from `false` to `true` to enable the ServiceProvider.

`check_enabled` is a feature which will check the connections for connectivity, it will update the `status` field in the connections table with a boolean value. Please note this could become resource intensive and increase page load times if you have a high amount of connections, it is disabled by default.

## Support

Please raise an issue on Github if there is a problem.

## License

This is open-sourced software licensed under the [MIT license](http://opensource.org/licenses/MIT).
