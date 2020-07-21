# Settings
## 1. Java
### 1.1 : Download the code
```
# 설치 가능한 자바 버전 확인
> yum list java*jdk-devel

# 자바 설치
> yum install java-1.8.0-openjdk-devel.x86_64

# 자바 버전 확인
> java -version
> rpm -qa java*jdk-devel
> javac -version
```
## 2. Maven
### 2.1 : Download Maven
```
# apps 폴더로 이동
> cd ~/apps

# Maven 다운로드 (Version 3.6.3)
> wget http://mirror.navercorp.com/apache/maven/maven-3/3.6.3/binaries/apache-maven-3.6.3-bin.tar.gz

# 압축해제
> tar -xvzf apache-maven-3.6.3-bin.tar.gz

# 파일 이동 & 링크 설정
> mv apache-maven-3.6.3 ~/src
> cd ~/src
> sudo ln -s apache-maven-3.6.3 maven
```
### 2.2 : Preferences
```
# maven 환경변수 설정 파일 생성
> vi /etc/profile.d/maven.sh

# 아래 내용을 저장
export MAVEN_HOME=/root/src/maven
export PATH=${PATH}:${MAVEN_HOME}/bin

# maven.sh 를 실행하여 적용
> source /etc/profile.d/maven.sh
```
### 2.3 : Check the installation
```
# maven 설치 확인
> mvn -version
```
## 3. Kafka
### 3.1 : Download the code
```
# kafka 설치
> cd ~/apps
> wget http://apache.mirror.cdnetworks.com/kafka/2.5.0/kafka_2.12-2.5.0.tgz
> tar -xvf kafka_2.12-2.5.0.tgz

# 디렉토리 이동 후 심볼릭 링크 설정
> mv kafka_2.12-2.5.0 ~/src
> cd ~/src
> ln -s Kafka_2.12-2.5.0/ kafka 
```
## 4. Zookeeper
### 4.1 : Download the code
```
# zookeeper 설치
> cd ~/apps
> wget wget http://apache.mirror.cdnetworks.com/zookeeper/zookeeper-3.6.1/apache-zookeeper-3.6.1-bin.tar.gz
> tar -xvf apache-zookeeper-3.6.1-bin.tar.gz

# 디렉토리 이동 후 심볼릭 링크 설정
> mv apache-zookeeper-3.6.1-bin ~/src
> cd ~/src
> ln -s apache-zookeeper-3.6.1-bin/ zookeeper
```
## 5. Install MariaDB
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