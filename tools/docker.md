Docker
===

## How a Docker Container work?
![SMPP Model](./images/docker-dev-view.png)
- A developer will first write the project code in a Docker file and then build an image from that file.
- This image will contain the entire project code.
- Now, you can run this Docker Image to create as many containers as you want.
- This Docker Image can be uploaded on Docker hub (It is basically a cloud repository for your Docker Images, you can keep it public or private).
- This Docker Image on the Docker hub, can be pulled by other teams such as QA or Prod.

## Some example use cases
#### Use mysql and phpmyadmin for dev
- Need docker images for [mysql](https://hub.docker.com/_/mysql/) and [phpmyadmin](https://hub.docker.com/r/phpmyadmin/phpmyadmin/), pull them from docker hub.
- Pull commands
```shell
$ docker pull mysql/mysql
$ docker pull phpmyadmin/phpmyadmin
```
- Run mysql server container
```shell
$ docker run --name mysql-server -e MYSQL_ROOT_PASSWORD=[PASSWORD] -d mysql:latest
```
- Run bash from container mysql
```shell
$ docker run -it mysql-server bash
```
- Run phpmyadmin container
```shell
$ docker run --name phpmyadmin -d --link mysql-server:db -p 8080:80 phpmyadmin/phpmyadmin
```
- View container running/runned.
```shell
$ docker ps [-a]
```
- Stop & Remove container
```shell
$ docker stop [CONTAINER_ID]
$ docker rm [CONTAINER_ID]
```

#### Issues with Phpmyadmin
- Issue: Host '172.18.0.1' is not allowed to connect to this MySQL server. [Link](https://github.com/docker-library/mysql/issues/275#issuecomment-292208567)

- Issue phpmyadmin on mysql 8.0: mysqli_real_connect(): The server requested authentication method unknown to the client [caching_sha2_password]. [Link](https://stackoverflow.com/questions/49948350/phpmyadmin-on-mysql-8-0)

#### First Mysql Bash
- View list user and their host

```
mysql> SELECT host, user FROM mysql.user;
```

- Alter user root password

```
mysql> ALTER USER 'root'@'localhost' IDENTIFIED BY 'newpassword';
```

- Create an user for accessing from any host.

```
mysql> CREATE USER 'someuser'@'%' IDENTIFIED BY 'userpassword';
```

- Fix issue unable login on phpmyadmin (mysql 8.0) (`caching_sha2_password`)

```
mysql> ALTER USER someuser IDENTIFIED WITH mysql_native_password BY 'userpassword';
```

- Create an database 'my_db'

```
mysql> CREATE DATABASE my_db;
```

- Grant all permission for user on a specify database

```
mysql> GRANT ALL ON my_db.* to 'someuser'@'%';
```

## References
- [What is the purpose of Docker](https://www.quora.com/What-is-the-purpose-of-Docker)
- [Docker for Beginners](https://docker-curriculum.com/#docker-images)