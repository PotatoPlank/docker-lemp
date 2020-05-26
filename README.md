# Simple Docker LEMP Stack

**This configuration is not production ready and is intended only for development!**

## Services
* Nginx
  * Binds to port 80 and 443.
* PHP-FPM
* MariaDB
  * Binds to port 3306
* Mailhog
  * Binds to port 8025.

## How to use this image
First, install Docker and Docker Compose.
Once Docker is installed, the services need to be built.

Next, change the default root password specified in docker-compose.yml.

```
$ docker-compose build
```

To start the services in detached mode:

```
$ docker-compose up -d
```