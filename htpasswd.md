# htpasswd

## 개요

docker registry에서는 이 방식을 이용해 유저 정보를 인증하는 부분을 통하여 학습하게 되었다..  

basic authentication에서 사용할 유저 계정, 비밀번호를 관리한다.  
기본적으로 일반적인 text파일로 젖아되며 데이터베이스를 위한 것도 존재한다.  

### 참고 사이트

[여기](https://httpd.apache.org/docs/2.4/programs/htpasswd.html)

## 사용

> htpasswd -c [파일명] [유저 아이디]

### 주의사항

웹에서 사용하는 기술인 만큼, 당연하게도 이 정보는 노출되어서는 안된다.   
window와 MPE? 플랫폼에서는 암호의 길이를 255자로 제한한다.
