# docker-registry

## 개요

도커는 https://hub.docker.com/ 를 통해 기본적으로 저장소를 제공한다. 이미 많은 오픈 소스들이 이를 통해 프로젝트 이미지들을 공유하고 있다. 하지만 공개 저장소이기 때문에 실제 프로젝트를 관리하게 될 경우 사직인 저장소가 필요하게 된다.  
https://hub.docker.com/ 에서도 1개의 기본 private 저장소를 제공하고 더 많은 private 저장소를 사용하기 위헤서는 유료모델을 사용하면 된다.  
다른 방법으로는 도커에서 공개한 오픈소스 프로젝트로서 docker-registry가 있다. 자신의 서버를 도커 이미지를 관리하게 할 수 있게 해주는 프로젝트다.


### 설치

### 도커 설치

원문은 [여기](https://docs.docker.com/install/linux/docker-ce/ubuntu/#install-using-the-repository)


기존의 도커 삭제
```
$ sudo apt-get remove docker docker-engine docker.io
```

https를 통한 apt를 사용하기 위한 패키지 설치
```
$ sudo apt-get install \
    apt-transport-https \
    ca-certificates \
    curl \
    software-properties-common
```

도커 공식 GPG키 획득 및 확인
```
$ curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -

$ sudo apt-key fingerprint 0EBFCD88

```

도커 CE 설치

```
$ sudo apt-get update && sudo apt-get install docker-ce
```




#### 또는

docker.io를 이용한 설치
```
$ apt-get install docker.io
```

### docker-registry

docker-registry 또한 docker를 통해 배포된다.


```
$ docker pull registry:latest
```



## 실행

```
$ docker run -d -p ${외부포트:내부포트} --name ${컨테이너이름} ${이미지이름}
```


## 작동

### push

```
docker push localhost:5000/${업로드할 이미지이름}
```

### pull
```
docker push localhost:5000/${풀 받을 이미지이름}
```

## 중지

```
$ docker container stop ${컨테이너이름} && docker container rm -v ${컨테이너이름}
```


계속..
