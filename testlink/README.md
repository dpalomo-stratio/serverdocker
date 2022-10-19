# Configuration

## Environment variables

When you start the testlink image, you can adjust the configuration of the instance by passing one or more environment variables either on the docker-compose file or on the docker run command line.

##### User and Site configuration

 - `TESTLINK_USERNAME`: TestLink admin username. Default: **user**
 - `TESTLINK_PASSWORD`: TestLink admin password. Default: **bitnami**
 - `TESTLINK_EMAIL`: TestLink admin email. Default: **user@example.com**
 - `TESTLINK_LANGUAGE`: TestLink default language. Default: **en_US**

##### Use an existing database

- `MARIADB_HOST`: Hostname for MariaDB server. Default: **mariadb**
- `MARIADB_PORT_NUMBER`: Port used by MariaDB server. Default: **3306**
- `TESTLINK_DATABASE_NAME`: Database name that TestLink will use to connect with the database. Default: **bitnami_testlink**
- `TESTLINK_DATABASE_USER`: Database user that TestLink will use to connect with the database. Default: **bn_testlink**
- `TESTLINK_DATABASE_PASSWORD`: Database password that TestLink will use to connect with the database. No defaults.
- `ALLOW_EMPTY_PASSWORD`: It can be used to allow blank passwords. Default: **no**

##### Create a database for TestLink using mysql-client

- `MARIADB_HOST`: Hostname for MariaDB server. Default: **mariadb**
- `MARIADB_PORT_NUMBER`: Port used by MariaDB server. Default: **3306**
- `MARIADB_ROOT_USER`: Database admin user. Default: **root**
- `MARIADB_ROOT_PASSWORD`: Database password for the `MARIADB_ROOT_USER` user. No defaults.
- `MYSQL_CLIENT_CREATE_DATABASE_NAME`: New database to be created by the mysql client module. No defaults.
- `MYSQL_CLIENT_CREATE_DATABASE_USER`: New database user to be created by the mysql client module. No defaults.
- `MYSQL_CLIENT_CREATE_DATABASE_PASSWORD`: Database password for the `MYSQL_CLIENT_CREATE_DATABASE_USER` user. No defaults.
- `ALLOW_EMPTY_PASSWORD`: It can be used to allow blank passwords. Default: **no**

If you want to add a new environment variable:

 * For docker-compose add the variable name and value under the application section in the  [`docker-compose.yml`](https://github.com/bitnami/bitnami-docker-testlink/blob/master/docker-compose.yml) file present in this repository:


```yaml
testlink:
  ...
  environment:
    - TESTLINK_PASSWORD=my_password
  ...
```

 * For manual execution add a `-e` option with each variable and value:

  ```bash
  $ docker run -d -p 80:80 -p 443:443 --name testlink
    -e TESTLINK_PASSWORD=my_password \
    --net testlink-tier \
    --volume /path/to/testlink-persistence:/bitnami/testlink \
    --volume /path/to/apache-persistence:/bitnami/apache \
    --volume /path/to/php-persistence:/bitnami/php \
    bitnami/testlink:latest
  ```

### SMTP Configuration

To configure TestLink to send email using SMTP you can set the following environment variables:

 - `SMTP_ENABLE`: Enable SMTP mail delivery.
 - `SMTP_HOST`: SMTP host.
 - `SMTP_PORT`: SMTP port.
 - `SMTP_USER`: SMTP account user.
 - `SMTP_PASSWORD`: SMTP account password.
 - `SMTP_CONNECTION_MODE`: SMTP connection mode, `ssl` or `tls`.

This would be an example of SMTP configuration using a GMail account:

 * For docker-compose add the variable name and value under the application section in the  [`docker-compose.yml`](https://github.com/bitnami/bitnami-docker-testlink/blob/master/docker-compose.yml) file present in this repository:

  ```yaml
  testlink:
    ...
    environment:
      - MARIADB_HOST=mariadb
      - MARIADB_PORT_NUMBER=3306
      - TESTLINK_DATABASE_USER=bn_testlink
      - TESTLINK_DATABASE_NAME=bitnami_testlink
      - SMTP_ENABLE=true
      - SMTP_HOST=smtp.gmail.com
      - SMTP_PORT=587
      - SMTP_USER=your_email@gmail.com
      - SMTP_PASSWORD=your_password
      - SMTP_CONNECTION_MODE=tls
    ...
  ```

 * For manual execution:

  ```bash
  $ docker run -d -p 80:80 -p 443:443 --name testlink \
    -e MARIADB_HOST=mariadb \
    -e MARIADB_PORT_NUMBER=3306 \
    -e TESTLINK_DATABASE_USER=bn_testlink \
    -e TESTLINK_DATABASE_NAME=bitnami_testlink \
    -e SMTP_ENABLE=true \
    -e SMTP_HOST=smtp.gmail.com -e SMTP_PORT=587 \
    -e SMTP_USER=your_email@gmail.com \
    -e SMTP_PASSWORD=your_password \
    -e SMTP_CONNECTION_MODE=tls \
    --net testlink-tier \
    --volume /path/to/testlink-persistence:/bitnami \
    bitnami/testlink:latest
  ```