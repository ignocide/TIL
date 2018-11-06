# Spring Cloud Config

## 개요

이름에서 보다 싶이 spring cloud를 이용한 Spring boot의 설정 파일 관리 서버이다.  
기본적으로는 여러 프로젝트에서 사용되는 설정 파일들에 대해서 관리를 용이하게 해준다.  
Config서버에서는 주로 git을 이용하여(다른 방식도 있다.) 설정파일을 관리,반환 해준다.  
Config클라이언트를 설정하게 되면 설정한 환경에 맞는 설정파일을 호출해 사용하게 된다.
MSA같은 경우 기본적으로 일일이 각각의 프로젝트에서 관리하는 불편함을 해소 할 뿐만 아니라, 사용되는 설정에 대하여 중복되어 사용되는 부분에 대한 문제도 쉽게 해결이 되게 해준다.

### 설치

```xml
<dependency>
   <groupId>org.springframework.cloud</groupId>
   <artifactId>spring-cloud-config-server</artifactId>
</dependency>
```

spring cloud를 이용하여 보안에 대한 부분도 추가 가능하다.

```xml
<dependency>
     <groupId>org.springframework.boot</groupId>
     <artifactId>spring-boot-starter-security</artifactId>
 </dependency>
```


### 설정 방법

```java
@EnableConfigServer
@SpringBootApplication
public class ConfigApplication {

    public static void main(String[] args) {
        SpringApplication.run(ConfigApplication.class, args);
    }
}
```



#### 로컬파일로 설정하여 사용하기

```yml
spring:
  profiles:
    active: native
  cloud:
    config:
      server:
        native:
          search-locations: classpath:/config
```

이렇게 두고 resources/config 하위에 설정 파일들을 작성하면 된다.
