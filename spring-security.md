# spring-security

전체 소스는 [여기](https://github.com/ignocide/msa-example)

## 개요

이번 msa 프로젝트 정리하며 spring security 에 대한 부분을 정리한다.  
회사 프로젝트에서는 spring boot 1을 사용하였지만 2에 들어가면서 방법이 바뀌게 되어 새로이 정리한다.

## 설치

*pom.xml*
```xml
...
  <dependency>
      <groupId>org.springframework.security.oauth.boot</groupId>
      <artifactId>spring-security-oauth2-autoconfigure</artifactId>
  </dependency>

  <dependency>
      <groupId>org.springframework.boot</groupId>
      <artifactId>spring-boot-starter-security</artifactId>
  </dependency>
...
```

## 설정

### 인증서버 설정

소스는 [여기](https://github.com/ignocide/msa-example/blob/master/auth-service/src/main/java/ignocide/msa/auth/config/AuthConfig.java)

```java
interface AuthorizationServerConfigurerAdapter
```

를 통해 인증서버를 구현한다.  
`@EnableAuthorizationServer` 어노테이션을 통해 Spring 컨텍스트에 등록한다.

#### 인증서버 엔드포인트 설정

```java
void configure(AuthorizationServerEndpointsConfigurer endpoints)
```

인증서버에 대해서 토큰 저장소, 사용자 승인 및 권한 유형, 인증 서버에서 제공하는 엔드포인트의 보안을 설정한다.

#### 보안 설정

```java
void configure(AuthorizationServerSecurityConfigurer security)
```

인증 서버의 인증 기능에 대한 설정을 한다. 즉. /oauth/token (기본값) 에 대한 설정을 한다.

#### 클라이언트 설정

```java
void configure(ClientDetailsServiceConfigurer clients)
```

보안서버에서 사용할 클라이언트들에 대한 설정을 한다.

구 버전에서는 이 부분에서 작성되는 secret에 대해서 암호화가 필요 없었지만 지금은 필수로 암호화를 하여 사용해야한다.

### 인증 설정

소스는 [여기](https://github.com/ignocide/msa-example/blob/master/auth-service/src/main/java/ignocide/msa/auth/config/SecurityConfig.java)

위와는 다르게 인증 로직, 방법 등에 대해서 설정한다.

#### 인증 로직

```java
void configure(AuthenticationManagerBuilder auth)
```

이 method로 전달된 인증 `요청`을 받아 `처리`하고 `권한이 부여된 객체를 반환`한다.


```java
void configure(HttpSecurity http)
```

들어오는 요청에 대해서 사용자의 인증에 대한 설정을 한다. 어느 요청에서는 어떠한 권한이 필요하다. form로그인, httpBasic로그인 등이 필요하다. 라는 등의 설정을 한다.


### 리소스 서버 설정

리소스 서버를 분리하고 리소스에 대한 보안 설정을 따로 한다. 소스는 [여기](https://github.com/ignocide/msa-example/blob/master/auth-service/src/main/java/ignocide/msa/auth/config/ResourceConfig.java)

```
void configure(HttpSecurity http)
```

를 구현하여 설정을 마친다. 설정에 대한 것은 위와 같다. 
