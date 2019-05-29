# docker-phpipam

phpIPAM is an open-source web IP address management application. Its goal is to provide light and simple IP address management application.

phpIPAM is developed and maintained by Miha Petkovsek, released under the GPL v3 license, project source is [here](https://github.com/phpipam/phpipam)

Learn more on [phpIPAM homepage](http://phpipam.net)

![phpIPAM logo](http://phpipam.net/wp-content/uploads/2014/12/phpipam_logo_small.png)

## How to use this Docker image

### Docker compose

You can create an all-in-one YAML deployment descriptor with Docker compose, for example:

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
    image: scrubs/phpipam:latest
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
