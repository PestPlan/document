## 1. Jenkins
Docker Hub 에서 Jenkins 이미지를 설치한다. 최근 버전 사용을 위해 lts 로 설치한다.
```
>> docker pull jenkins/jenkins:lts
```
설치된 이미지는 아래 명령어를 통해 확인할 수 있다.
```
>> docker images
```
Jenkins 이미지를 실행한다.
```
>> docker run -d -p 8181:8080 -p 50000:50000 -v jenkins_home:/var/jenkins_home --name jc_jenkins -u root jenkins/jenkins:lts
	[Options]
	-d						백그라운드 모드로 실행
	-p						호스트:컨테이너 포트 포워딩
	-v						호스트:컨테이너 디렉토리를 마운트
	--name					컨테이너의 이름을 설정
	-u						실행할 사용자를 설정
	jenkins/jenkins:lts		실행할 이미지의 레포지토리 이름이다. 만약 이름이 없을 경우, 이미지를 Docker Hub 에서 설치 후 실행하므로 주의한다.
```
실행 중인 컨테이너 목록은 아래 명령어를 통해 확인할 수 있다.
```
>> docker ps  // 실행 중이지 않은 컨테이너 목록까지 보고싶다면 -a 옵션을 추가한다.
```
----------
## 2. Elasticsearch
Docker Hub 에서 Elasticsearch 7.9.2. 버전을 설치한다.
```
>> docker pull docker.elastic.co/elasticsearch/elasticsearch:7.9.2
```
Elasticsearch 이미지를 single-node 로 실행한다.
```
>> docker run -p 9200:9200 -p 9300:9300 -e "discovery.type=single-node" docker.elastic.co/elasticsearch/elasticsearch:7.9.2
```
----------
## 3. Kafka & Zookeeper with docker-compose
kafka-and-zookeeper.yml 파일을 생성한다. (파일의 이름은 변경 가능하다)

파일에는 아래 내용을 적는다.
```
version: '3'

services:
  zoo1:
    image: zookeeper:3.6.1
    restart: always
    hostname: zoo1
    ports:
      - "2181:2181"
    environment:
      ZOO_MY_ID: 1
      ZOO_SERVERS: server.1=0.0.0.0:2888:3888;2181 server.2=zoo2:2888:3888;2181 server.3=zooe:2888:3888;2181

  zoo2:
    image: zookeeper:3.6.1
    restart: always
    hostname: zoo2
    ports:
      - "2182:2181"
    environment:
      ZOO_MY_ID: 2
      ZOO_SERVERS: server.1=zoo1:2888:3888;2181 server.2=0.0.0.0:2888:3888;2181 server.3=zoo3:2888:3888;2181

  zoo3:
    image: zookeeper:3.6.1
    restart: always
    hostname: zoo3
    ports:
      - "2183:2181"
    environment:
      ZOO_MY_ID: 3
      ZOO_SERVERS: server.1=zoo1:2888:3888;2181 server.2=zoo2:2888:3888;2181 server.3=0.0.0.0:2888:3888;2181

  kafka1:
    image: wurstmeister/kafka:2.12-2.5.0
    ports:
      - "9092:9092"
    environment:
      KAFKA_BROKER_ID: 1
      KAFKA_ADVERTISED_LISTENERS: PLAINTEXT://34.64.155.139:9092
      KAFKA_LISTENERS: PLAINTEXT://0.0.0.0:9092
      KAFKA_ZOOKEEPER_CONNECT: zoo1:2181,zoo2:2181,zoo3:2181/caps
      KAFKA_CREATE_TOPICS: "test-topic:3:1"
      KAFKA_LOG_DIRS: /kdata
    volumes:
      - /var/run/docker.sock:/var/run/docker.sock
```
docker-compose를 통해 kafka-and-zookeeper.yml의 설정으로 Kafka와 Zookeeper를 설치한다.
```
>> docker-compose -f kafka-and-zookeeper.yml up -d
```