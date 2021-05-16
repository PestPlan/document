## 1. Python (3.X)
### 1.1: Python 3.X 버전 설치
현재 설치된 파이썬의 버전과 위치를 파악한다.

```
> python -V
> which python
```

python3를 설치한다 (yum install 기준 3.6버전 설치)

```
> yum install python3
> python3 -V
```
```
Python 3.6.8
```

### 1.2: Python, pip Symbolic link 변경
```
> update-alternatives --config python (미설정 시, 아무것도 뜨지않는다.)
```
```
> update-alternatives --install /bin/python python /bin/python2.7 1
> update-alternatives --install /bin/python python /bin/python3.6 2
```
위 두 커맨드 입력 이후, 2번을 선택한다 (python3.6)

pip의 경로 또한 변경한다.
```
> ln -s /bin/pip3.6 /bin/pip
> pip -V
```

위 과정을 거치면 기존 yum의 사용이 불가능해진다. 따라서 yum의 설정 또한 변경한다.

```
> vi /usr/bin/yum
> #!/usr/bin/python -> #!/usr/bin/python2.7

> vi /usr/libexec/urlgrabber-ext-down
> #!/usr/bin/python -> #!/usr/bin/python2.7

```

----------



## 2 MongoDB
### 2.1: Repository 등록

```
> yum search mongodb
> vi /etc/yum.repos.d/mongodb.repo
 
[MongoDB]
name=MongoDB Repository
baseurl=http://repo.mongodb.org/yum/redhat/$releasever/mongodb-org/4.2/$basearch/
gpgcheck=1
enabled=1
gpgkey=https://www.mongodb.org/static/pgp/server-4.2.asc

(저장)

```
### 2.2: MongoDB 설치
```
> yum install mongodb-org
```

### 2.3: systemctl 등록/실행
```
> systemctl start mongod
> systemctl enable mongod
```

### 2.4: 세부 설정
```
> systemctl edit mongod
> 
[Service]
PermissionsStartOnly=true
ExecStartPre=/bin/sh -c "echo never > /sys/kernel/mm/transparent_hugepage/enabled"
> systemctl restart mongod
```
### 2.5: 계정 생성 및 인증
```
> mongo
> show dbs;
> use admin
> db.createUser(
... {
... user: "mongoUserAdmin",
... pwd: "yourpwd",
... roles: [{role: "userAdminAnyDatabase", db: "admin"}]
... }
... )
Successfully added user: {
        "user" : "mongoUserAdmin",
        "roles" : [
                {
                        "role" : "userAdminAnyDatabase",
                        "db" : "admin"
                }
        ]
}
```

### 2.6: 외부 IP 접근 허용
```
 > vi /etc/mongod.conf
 > #network interfaces
 > net:
    bindIp: 127.0.0.1 --> 0.0.0.0
```

----------