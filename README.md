# Captiv8 Back-End

## Getting Started

 This repository contains the back-end part of the [Captiv8](https://captiv8.io/) interactive web
application. It uses 
 * [`Laravel`](https://laravel.com/) as a main PHP framework. 
 * [`Composer`](https://getcomposer.org/) is a tool for dependency management.
 * [`Redis`](https://redis.io/) as an advanced key-value store and Memcached as an in-memory key-value store for small chunks of arbitrary data (strings, objects) from results of database calls, API calls.
 * Laravel migrations are like version control for database, allowing easily modify and share the application's database schema.
 * Laravel queues provide a unified API across a variety of different queue backends. Queues allow you to defer the processing of a time consuming task.
 * Project uses [`Centrifugo`](https://github.com/centrifugal/centrifugo) as a real-time messaging server. Centrifugo runs as separate service and keeps persistent Websocket or SockJS connections from application clients browsers. When some event happens you can broadcast it to all interested clients using Centrifugo API.
[Documentation](http://fzambia.gitbooks.io/centrifugal/content/) is a good start to get all details.

### Requirements

* PHP >= 7.1.3
  * OpenSSL PHP Extension
  * PDO PHP Extension
  * Mbstring PHP Extension
  * Tokenizer PHP Extension
  * XML PHP Extension
  * Ctype PHP Extension
  * JSON PHP Extension
* Composer >= 1.6.4
* Centrifugo >= 1.7.9
* MariaDB >= 10.0.34
* Beanstalkd >= 1.10
* Supervisor >= 3.2.0
* Nginx >= 1.13.6
* Redis
* Memcached
* ElasticSeach = 5.6.3


### How to install

```shell
$ git clone git@github.com:captiv8io/captiv8io.git
$ composer install
$ php artisan migrate
$ php artisan db:seed
```
### Supervisor config exmaple:

```shell
$ [program:captiv8-1]
$ command=php /home/c8prod/captiv8.io/artisan queue:work beanstalkd --sleep=10 --daemon --quiet --tries=3 --$ queue="production"
$ stdout_logfile=/home/vagrant/captiv8.io/storage/logs/supervisord/captiv8.log
$ redirect_stderr=true
$ autostart=true
$ autorestart=true
$ user=vagrant
```

Queue workers list:

| queue prefix       | How to start   | Description          |
| ---------- | ------------- | -------------------------- |
| `ac_tokens_check`    | php artisan access_token:check | Validate access tokens                         |
| `cio`     | - | Events for customer.io                |
| `digest`      | - | -                |
| `es`     | - | Events for ElasticSearch |
| `es_calc`    | php artisan discovery_es_index:send | Data calculation for ElasticSearch                          |
| `fb_main`   | -   | -                          |
| `g_c`     | -   | Project garbage collector                          |
| `mp_default` | -   | Events for discovery                          |
| `mp_inf_update_main	`     | php artisan marketplace:start   | Calculation profiles for discovery                          |
| `mp_post_update`    |  php artisan marketplace_post:start   | Calculation posts for discovery                           |
| `post_monitor`     | php artisan post_monitor:start   | Start collect data for auto campaigns                          |
| `production`    | -   | Events for insights                          |


## Directory Structure

`app/`: Contains the core code.

  The most significant directories into `app/` 
   * The Console Directory - console tasks
   * The Helpers Directory - useful functions
   * The Exceptions Directory
   * The Http Directory - Controllers, Middlewares, Routes
   * The Jobs Directory - All asynchronous tasks
   * The Models Directory - Eloquent ORM models
   * The Servises Directory - Various classes for business logic etc.
   * The Sources Directory - Various classes for business logic etc.
   * The Traits Directory - List of traits.
   * The Validators Directory - Captiv8 custom validators.

`bootstrap/`: contains the app.php file which bootstraps the framework. This directory also houses a cache directory which contains framework generated files.

`config/`: contains all of application's configuration files.

`database/`: contains database migrations, model factories, and seeds.

`public/`: the entry point for most requests, also houses assets (js, css, image).

`resources/`: houses all of language files.

`storage/`: contains various auxiliary files.

`tests/`: contains automated tests.

`vendor/`: contains composer dependencies.

## Workflow

* When you start working on new task, create a new branch with the following format:
  `<prefix>/CE-<task number>`. Prefix may be one of:

| prefix        | description                                                                                                      |
| ------------- | ---------------------------------------------------------------------------------------------------------------- |
| `feature`     | use it if you add some new functionality or improvement                                                                                                     |
| `hotfix`      | some corrections into production (e.g. [`master`](https://github.com/captiv8io/captiv8io/tree/master) branch)         |


> Example: `feature/CE-3658`

## Code Style

[`psr-2`](https://www.php-fig.org/psr/psr-2/)

