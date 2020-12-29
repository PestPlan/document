# Settings
----------
## 1. Java
### 1.1 : Install
아래 명령어를 통해 Java 1.8.0 을 설치한다.
```
> yum install java-1.8.0-openjdk-devel.x86_64
```
Java 버전 정보는 아래 3가지 명령어 중 하나를 실행하여 확인할 수 있다.
```
> java -version
> rpm -qa java*jdk-devel
> javac -version
```
----------
## 2. Maven (Version 3.6.3)
### 2.1 : Download Maven
Maven 압축파일을 다운로드 받아 압축을 해제한다.
```
> cd ~/apps
> wget http://mirror.navercorp.com/apache/maven/maven-3/3.6.3/binaries/apache-maven-3.6.3-bin.tar.gz
> tar -xvzf apache-maven-3.6.3-bin.tar.gz
```
압축해제한 Maven 파일을 디렉토리 이동 후 심볼릭 링크를 설정한다. 심볼릭 링크는 Maven의 버전이 변경되었을 때 링크만 변경하여 내용을 적용하기 위해 사용된다.
```
> mv apache-maven-3.6.3 ~/src
> cd ~/src
> sudo ln -s apache-maven-3.6.3 maven
```
### 2.2 : Preferences
Maven 환경변수 설정 파일을 생성한다.
```
> vi /etc/profile.d/maven.sh
```
```
export MAVEN_HOME=/home/capstonegcp/src/maven
export PATH=${PATH}:${MAVEN_HOME}/bin
```
위의 내용을 저장 후 maven.sh 파일을 실행하여 설정을 적용한다.
```
> source /etc/profile.d/maven.sh
```
### 2.3 : Check the installation
Maven 버전 정보를 확인하여 설치유무를 확인한다.
```
> mvn -version
```
----------
## 5. MariaDB
### 5.1 : Download the code
```
# MariaDB 설치를 위한 사전설정
> vi /etc/yum.repos.d/MariaDB.repo
	#아래 내용 추가
	[mariadb]
	name = MariaDB
	baseurl = http://yum.mariadb.org/10.5/centos7-amd64
	gpgkey=https://yum.mariadb.org/RPM-GPG-KEY-MariaDB
	gpgcheck=1
	
# MariaDB 설치
> yum install MariaDB

# MariaDB 설치 확인
> rpm -qa | grep MariaDB

# 부팅시 자동시작 설정
> systemctl enable mairadb

# 설정 확인
> systemctl is-enabled mariadb
```
### 5.2 : Create & Configure DB
- 로컬에서 접속할 경우 : localhost
- 원격 접속할 경우 : % 
```
# MariaDB 접속
> mysql -u @username -p
> Enter password: @password

# DB 생성
> create database @dbname;

# 계정 생성
> create user 'username'@'loaclhost' identified 'password';
> create user 'username'@'%' identified by 'password';

#계정 조회
> select host, user, from mysql.user;

# 유저에게 권한 부여
> grant all privileges on dbname.* to 'username'@'localhost';
> grant all privileges on dbname.* to 'username'@'%';
> flush privileges;

# 권한 조회
> show grants for 'username'@'localhost';
> show grants for 'username'@'%';
```
----------
## 6. Node.js
### 6.1 : EPEL repository
```
# epel repository 확인
> yum repolist

# epel repository 설치
> yum install epel-release
```
### 6.2 : Intsall Node.js
```
# Node.js 설치
> yum install nodejs
```
### 6.3 : Check the installation
```
# Node.js 설치 확인
> node -v

# npm 설치 확인
> npm -v
```
### 6.4 : Upgrade to the latest version
```
# Cache 삭제
> sudo npm cache clean -f

# n 설치
> sudo npm install -g n

# 최신버전으로 업그레이드
> n latest
```
----------
## 7. Docker
Docker 설치를 하기 전에 필요한 패키지와 저장소를 먼저 설치한다.
```
> yum install -y yum-utils device-mapper-persistent-data lvm2
> yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo
> yum update
```
Docker 를 설치한다.
```
> yum install -y docker-ce
```