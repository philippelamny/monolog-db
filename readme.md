## Laravel 6.x Monolog Database Handler.

This package will log errors into a database instead storage/log/laravel.log file.

### Installation

~~~
composer require philippelamny/monolog-db
~~~

Open up `config/logging.php` and find the `channels` key. Add the following channel to the list.

~~~
'database' => [
    'driver' => 'custom',
    'via'=> \Logger\DatabaseLogger::class,
    'table'=> env('DB_LOG_TABLE', 'logs'),
    'connection' => env('DB_LOG_CONNECTION', env('DB_CONNECTION', 'mysql')),
],
~~~

Set up Environment Variables (see Below).

Migrate the tables.

~~~
php artisan migrate
~~~

## Database Engines

Make sure before you migrate the table that you have set the envirment veriable for the database engine. This is done by adding the following line to the `.env` file
~~~
DB_LOG_ENGINE=InnoDB
~~~

To use the whatever the default database engine is or to specify no database engine during the table migration use the following
~~~
DB_LOG_ENGINE=NONE
~~~

## Environment configuration

If you wish to change default table name to write the log into add the following definition in your `.env` file

~~~
DB_LOG_TABLE=logs
~~~

To change the database connection that is used to wright the logs add the following definition to your `.env` file
~~~
DB_LOG_CONNECTION=mysql
~~~

To make sure you are using the `database` channel for logging add it to the stack in your `config\logging.php` or change the following in your `.env` file

~~~
LOG_CHANNEL=database
~~~

## Credits

Based on:

- [Mark Hilton] (https://github.com/markhilton/monolog-mysql)
- [Pedro Fornaza] (https://github.com/pedrofornaza/monolog-mysql)
