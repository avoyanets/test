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


### How to install





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
