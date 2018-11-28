# spring boot dockerize (도커파일 만들기)

## 개요

spring boot에서 도커화 시키는 방법을 알아본다.

### 설치

pom.xml에 빌드에 대한 설정을 해준다. spotify의 dockerfile플러그인을 사용한다.

```xml
<!--pom.xml-->

...
<build>
    <plugins>
        <plugin>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-maven-plugin</artifactId>
        </plugin>
        <plugin>
            <groupId>com.spotify</groupId>
            <artifactId>dockerfile-maven-plugin</artifactId>
            <version>1.3.6</version>
            <configuration>
                <repository>${docker.image.prefix}/${project.artifactId}</repository>
            </configuration>
        </plugin>
    </plugins>
</build>
```

Dockerfile 작성한다.
ENV를 통해 환경을 지정해준다.

```text
//Dockerfile
FROM openjdk:8-jdk-alpine
VOLUME /tmp
COPY {타겟이 되는 jar파일} app.jar
ENV JAVA_OPTS="-Dspring.profiles.active=development"
ENTRYPOINT ["java","-Djava.security.egd=file:/dev/./urandom","-jar","/app.jar"]
```


### build

> /mvnw install dockerfile:build

또는 ide에서 bulid 실행  

### 실행

```yml
# docker-compsoe.yml
version: '3'

services:
    discovery-service:
        restart: always
        image: {docker.image.prefix}/${project.artifactId}
        ports:
            - {port}:{port}
```
