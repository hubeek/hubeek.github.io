# Docker

_Status: Published_
_Created: 2017-05-05 16:01:59_
_Tags: terminal, docker_

<h2>cleanup</h2>
~/Library/Containers/com.docker.docker/Data/com.docker.driver.amd64-linux/Docker.qcow2
never shrinks...

<h2>Dockerfile recipes</h2>

<h3>Java hello</h3>
<code>
FROM openjdk:14-alpine
COPY out/artifacts/testdockerhello_jar/testdockerhello.jar /usr/src/hello.jar
CMD java -cp /usr/src/hello.jar Main
</code>

<h3>Spring basic</h3>
with maven pom.
<code>
<build>
        <plugins>
            <plugin>
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-maven-plugin</artifactId>
            </plugin>
        </plugins>
        <finalName>docker-spring-demo</finalName>
    </build>
</code>
Dockerfile
<code>
FROM openjdk:11

EXPOSE 8080

ADD target/docker-spring-demo.jar app.jar

ENTRYPOINT ["java","-jar", "app.jar"]
</code>

<h2>Mysql recipe</h2>
<code>
docker run --name mysql -e MYSQL_USER=user -e MYSQL_PASSWORD=password -e MYSQL_DATABASE=databasename -p 3306:3306 -d mysql/mysql-server
</code>

<h2>Sails</h2>
run sails from local dir in docker conatiner
<code>docker container run -it -p 1337:1337 -v $(pwd):/server artificial/docker-sails /bin/bash</code>

<h2>Swift</h2>
run docker app
then
<code>
docker pull swift
docker pull postgres:alpine

docker container run -d -p 3306:3306 --name mysql -e MYSQL_RANDOM_ROOT_PASSWORD=yes  mysql
docker container run --name mysql -p 3306:3306 -e MYSQL_RANDOM_ROOT_PASSWORD=yes -d mysql
docker container logs mysql
docker exec -it mysql bash -l

docker container run -d --name mysql -e MYSQL_ROOT_PASSWORD=root -p 3306 -v /Users/lappie2010/Documents/docker/mysql/:/var/lib/mysql mysql


docker container logs mysql

docker container run -d --name webserver -p 8080:80 httpd

docker container run -d --name proxy -p 80:80 nginx


docker run --cap-add sys_ptrace -it --privileged=true swift bash
</code>

<h2>Docker Mysql + Wordpress </h2>
<code>
docker container run -d \
    --name wordpress \
--link mysql:mysql\
    -p 8080:80 \
    -e WORDPRESS_DB_PASSWORD=root \
    wordpress

    docker container run -d \
        --name mysql \
        -e MYSQL_ROOT_PASSWORD=root \
        -e MYSQL_DATABASE=wordpress \
        mysql

</code>