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
- Remove container
```shell
$ docker rm [CONTAINER_ID]
```

## References
- [What is the purpose of Docker](https://www.quora.com/What-is-the-purpose-of-Docker)
- [Docker for Beginners](https://docker-curriculum.com/#docker-images)