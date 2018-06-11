# Captiv8 Back-End

## Getting Started

This repository contains the back-end part of the [Captiv8](https://captiv8.io/) interactive web
application. It uses [`Laravel`](https://laravel.com/) as a main framework.

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


### How to install

```shell
$ git clone git@github.com:captiv8io/captiv8io.git
$ composer install
$ php artisan migrate
$ php artisan db:seed
```
Supervisor config exmaple:

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


Centrifugo is a real-time messaging server. Version 1.7.9 (https://github.com/centrifugal/centrifugo)
### How to install

Releases available as single executable files – just [download latest release](https://github.com/centrifugal/centrifugo/releases) for your platform, unpack and run.

If you are on MacOS:

```
brew tap centrifugal/centrifugo https://github.com/centrifugal/centrifugo
brew install centrifugo
```

See official [Docker image](https://hub.docker.com/r/centrifugo/centrifugo/) and [Kubernetes Helm Chart](https://github.com/kubernetes/charts/tree/master/stable/centrifugo).

There are also [packages for 64-bit Debian, Centos and Ubuntu](https://packagecloud.io/FZambia/centrifugo).
