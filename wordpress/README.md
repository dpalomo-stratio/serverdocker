
# Configuration

## Environment variables

The WordPress instance can be customized by specifying environment variables on the first run. The following environment values are provided to custom WordPress:

##### User and Site configuration

- `WORDPRESS_USERNAME`: WordPress application username. Default: **user**
- `WORDPRESS_PASSWORD`: WordPress application password. Default: **bitnami**
- `WORDPRESS_EMAIL`: WordPress application email. Default: **user@example.com**
- `WORDPRESS_FIRST_NAME`: WordPress user first name. Default: **FirstName**
- `WORDPRESS_LAST_NAME`: WordPress user last name. Default: **LastName**
- `WORDPRESS_BLOG_NAME`: WordPress blog name. Default: **User's blog**
- `WORDPRESS_SCHEME`: Scheme to generate application URLs. Default: **http**
- `WORDPRESS_HTACCESS_OVERRIDE_NONE`: Set the Apache `AllowOverride` variable to `None`. All the default directives will be loaded from `/opt/bitnami/wordpress/wordpress-htaccess.conf`. Default: **yes**.

##### Use an existing database

- `MARIADB_HOST`: Hostname for MariaDB server. Default: **mariadb**
- `MARIADB_PORT_NUMBER`: Port used by MariaDB server. Default: **3306**
- `WORDPRESS_DATABASE_NAME`: Database name that WordPress will use to connect with the database. Default: **bitnami_wordpress**
- `WORDPRESS_TABLE_PREFIX`: Table prefix to use in WordPress. Default: **wp_**
- `WORDPRESS_DATABASE_USER`: Database user that WordPress will use to connect with the database. Default: **bn_wordpress**
- `WORDPRESS_DATABASE_PASSWORD`: Database password that WordPress will use to connect with the database. No defaults.
- `WORDPRESS_SKIP_INSTALL`: Force the container to not execute the WordPress installation wizard. This is necessary in case you use a database that already has WordPress data. Default: **no**
- `ALLOW_EMPTY_PASSWORD`: It can be used to allow blank passwords. Default: **no**

##### Create a database for WordPress using mysql-client

- `MARIADB_HOST`: Hostname for MariaDB server. Default: **mariadb**
- `MARIADB_PORT_NUMBER`: Port used by MariaDB server. Default: **3306**
- `MARIADB_ROOT_USER`: Database admin user. Default: **root**
- `MARIADB_ROOT_PASSWORD`: Database password for the `MARIADB_ROOT_USER` user. No defaults.
- `MYSQL_CLIENT_CREATE_DATABASE_NAME`: New database to be created by the mysql client module. No defaults.
- `WORDPRESS_TABLE_PREFIX`: Table prefix to use in WordPress. Default: **wp_**
- `MYSQL_CLIENT_CREATE_DATABASE_USER`: New database user to be created by the mysql client module. No defaults.
- `MYSQL_CLIENT_CREATE_DATABASE_PASSWORD`: Database password for the `MYSQL_CLIENT_CREATE_DATABASE_USER` user. No defaults.
- `ALLOW_EMPTY_PASSWORD`: It can be used to allow blank passwords. Default: **no**

### Specifying Environment variables using Docker Compose

This requires a minor change to the [`docker-compose.yml`](https://github.com/bitnami/bitnami-docker-wordpress/blob/master/docker-compose.yml) file present in this repository:

```yaml
services:
  mariadb:
  ...
    environment:
      - MARIADB_USER=bn_wordpress
      - MARIADB_DATABASE=bitnami_wordpress
      - ALLOW_EMPTY_PASSWORD=yes
  ...
  wordpress:
  ...
    environment:
      - MARIADB_HOST=mariadb
      - MARIADB_PORT_NUMBER=3306
      - WORDPRESS_DATABASE_USER=bn_wordpress
      - WORDPRESS_DATABASE_NAME=bitnami_wordpress
      - ALLOW_EMPTY_PASSWORD=yes
  ...
```

### Specifying Environment variables on the Docker command line

```bash
$ docker run -d --name wordpress -p 80:80 -p 443:443 \
  --net wordpress-tier \
  -e ALLOW_EMPTY_PASSWORD=yes \
  -e WORDPRESS_DATABASE_USER=bn_wordpress \
  -e WORDPRESS_DATABASE_NAME=bitnami_wordpress \
  -e WORDPRESS_PASSWORD=my_password \
  --volume wordpress_data:/bitnami \
  bitnami/wordpress:latest
```

### SMTP Configuration

To configure WordPress to send email using SMTP you can set the following environment variables:
- `SMTP_HOST`: Host for outgoing SMTP email. No defaults.
- `SMTP_PORT`: Port for outgoing SMTP email. No defaults.
- `SMTP_USER`: User of SMTP used for authentication (likely email). No defaults.
- `SMTP_PASSWORD`: Password for SMTP. No defaults.
- `SMTP_PROTOCOL`: Secure connection protocol to use for SMTP [tls, ssl, none]. No defaults.

This would be an example of SMTP configuration using a GMail account:

 * Modify the [`docker-compose.yml`](https://github.com/bitnami/bitnami-docker-wordpress/blob/master/docker-compose.yml) file present in this repository:

```yaml
  wordpress:
    ...
    environment:
      - MARIADB_HOST=mariadb
      - MARIADB_PORT_NUMBER=3306
      - WORDPRESS_DATABASE_USER=bn_wordpress
      - WORDPRESS_DATABASE_NAME=bitnami_wordpress
      - SMTP_HOST=smtp.gmail.com
      - SMTP_PORT=587
      - SMTP_USER=your_email@gmail.com
      - SMTP_PASSWORD=your_password
      - SMTP_PROTOCOL=tls
    ...
```

* For manual execution:

```bash
$ docker run -d --name wordpress -p 80:80 -p 443:443 \
  --net wordpress-tier \
  --env SMTP_HOST=smtp.gmail.com --env SMTP_PORT=587 \
  --env SMTP_USER=your_email@gmail.com --env SMTP_PASSWORD=your_password \
  --env ALLOW_EMPTY_PASSWORD=yes --env WORDPRESS_DATABASE_USER=bn_wordpress \
  --env WORDPRESS_DATABASE_NAME=bitnami_wordpress \
  --volume wordpress_data:/bitnami/wordpress \
  bitnami/wordpress:latest
```

### Connect WordPress docker container to an existing database

The Bitnami WordPress container supports connecting the WordPress application to an external database. In order to configure it, you should set the following environment variables:
- `MARIADB_HOST`: Hostname for MariaDB server. Default: **mariadb**
- `MARIADB_PORT_NUMBER`: Port used by MariaDB server. Default: **3306**
- `WORDPRESS_DATABASE_NAME`: Database name that WordPress will use to connect with the database. Default: **bitnami_wordpress**
- `WORDPRESS_DATABASE_USER`: Database user that WordPress will use to connect with the database. Default: **bn_wordpress**
- `WORDPRESS_DATABASE_PASSWORD`: Database password that WordPress will use to connect with the database. No defaults.
- `WORDPRESS_DATABASE_SSL_CA_FILE`: Certificate to connect with the  database using SSL. No defaults.

This would be an example of using an external database for WordPress.

 * Modify the [`docker-compose.yml`](https://github.com/bitnami/bitnami-docker-wordpress/blob/master/docker-compose.yml) file present in this repository:

```yaml
  wordpress:
    ...
    environment:
      - MARIADB_HOST=mariadb_host
      - MARIADB_PORT_NUMBER=3306
      - WORDPRESS_DATABASE_NAME=wordpress_db
      - WORDPRESS_DATABASE_USER=wordpress_user
      - WORDPRESS_DATABASE_PASSWORD=wordpress_password
    ...
```

* For manual execution:

```bash
$ docker run -d --name wordpress -p 80:80 -p 443:443 \
  --net wordpress-tier \
  --env MARIADB_HOST=mariadb_host \
  --env MARIADB_PORT_NUMBER=3306 \
  --env WORDPRESS_DATABASE_NAME=wordpress_db \
  --env WORDPRESS_DATABASE_USER=wordpress_user \
  --env WORDPRESS_DATABASE_PASSWORD=wordpress_password \
  --volume wordpress_data:/bitnami \
  bitnami/wordpress:latest
```

In case the database already contains data from a previous WordPress installation, you need to set the variable `WORDPRESS_SKIP_INSTALL` to `yes`. Otherwise, the container would execute the installation wizard and could modify the existing data in the database. Note that, when setting `WORDPRESS_SKIP_INSTALL` to `yes`, the values `WORDPRESS_USERNAME`, `WORDPRESS_PASSWORD`, `WORDPRESS_BLOG_NAME`, `WORDPRESS_EMAIL`, `WORDPRESS_BLOG_NAME` and `WORDPRESS_SMTP_*` variables will be ignored. Make sure that, in this imported database, the table prefix matches the one set in `WORDPRESS_TABLE_PREFIX`.

## WP-CLI tool

The Bitnami WordPress container includes the command line interface **wp-cli** that can help you to manage and interact with your WP sites. To run this tool, please note you need use the proper system user, **daemon**.

This would be an example of using **wp-cli** to display the help menu:

* Using `docker-compose` command:

```bash
$ docker-compose exec wordpress sudo -u daemon -- wp help
```

* Using `docker` command:

```bash
$ docker exec wordpress sudo -u daemon -- wp help
```

