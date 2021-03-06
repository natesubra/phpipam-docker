# docker-phpipam

phpIPAM is an open-source web IP address management application. Its goal is to provide light and simple IP address management application.

phpIPAM is developed and maintained by Miha Petkovsek, released under the GPL v3 license, project source is [here](https://github.com/phpipam/phpipam)

Learn more on [phpIPAM homepage](http://phpipam.net)

![phpIPAM logo](http://phpipam.net/wp-content/uploads/2014/12/phpipam_logo_small.png)

## Links to this image and image build process

[Dockerhub](https://hub.docker.com/r/scrubs/phpipam-docker) | [GitHub](https://www.github.com/natesubra/phpipam-docker)

## Changes

### release-v1.3.2

* Update dependency [php-saml](https://github.com/onelogin/php-saml) to v3.1.1
* Update dependency [PHPMailer](https://github.com/PHPMailer/PHPMailer) to v6.0.7
* Update dockerfile, removed autoremove, apt-get clean, added noninteractive variable

## How to use this Docker image

### Docker compose

You can create an all-in-one YAML deployment descriptor with Docker compose, for example:

docker-compose.yml:

```yaml
version: '3'

services:
  mysql:
    image: mariadb:latest
    container_name: phpipam_mysql_1
    environment:
      - MYSQL_ROOT_PASSWORD=super_secret_pass
    restart: unless-stopped
    volumes:
      - ./mysql:/var/lib/mysql

  ipam:
    depends_on:
      - mysql
    image: scrubs/phpipam-docker:latest
    environment:
      - MYSQL_ENV_MYSQL_USER=root
      - MYSQL_ENV_MYSQL_PASSWORD=super_secret_pass
      - MYSQL_ENV_MYSQL_HOST=phpipam_mysql_1
    restart: unless-stopped
    ports:
      - "80:80"

```

And next :

```bash
$ docker-compose up -d
```
