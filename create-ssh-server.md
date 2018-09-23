
# server

## install openssh

```
sudo apt-get update
sudo apt-get upgrade

sudo apt-get install openssh-server
```

### configure openssh-server

```
sudo nano /etc/ssh/sshd_config
```


# client

## create account for ssh-client

```
sudo adduser
```


## connect to ssh-server

```
sudo [account]@[ssh-server-host]
```




# use ssh-key

## change ssh-server config

```
RSAAuthentication yes
PubkeyAuthentication yes

ChallengeResponseAuthentication no
PasswordAuthentication no
UsePAM no
```

```
sudo service ssh restart
```
굳이 안해도 된다.
비밀번호로 로그인하는 옵션 끄는것

## client

```
cd ~/.ssh
ssh-keygen -t rsa
```

## server

생성된 id_rsa.pub의 값을 authorized_keys에 저장  

```
cd ~/.ssh
nano authorized_keys
// client의 id_rsa.pub의 값 추가로 작성
```
