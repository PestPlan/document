## 3. Kafka
### 3.1 : Specify the host name
hosts 파일을 수정한다.
```
> sudo vi /etc/hosts
```
```
34.64.239.98	zookeeper1
```
자기 자신은 **0.0.0.0** 으로 다른 서버는 각각의 IP와 호스트명을 등록하여 세팅한다.
### 3.2 : Download the code
Kafka 압축파일을 다운로드 받아 압축을 해제한다.
```
> cd ~/apps
> wget http://apache.mirror.cdnetworks.com/kafka/2.5.0/kafka_2.12-2.5.0.tgz
> tar -xvf kafka_2.12-2.5.0.tgz
```
압축해제한 Kafka 파일을 디렉토리 이동 후 심볼릭 링크를 설정한다.
```
> mv kafka_2.12-2.5.0 ~/src
> cd ~/src
> ln -s Kafka_2.12-2.5.0/ kafka 
```
### 3.3 : Make data file
카프카의 메시지를 저장할 디렉토리 파일을 생성한다.
```
> mkdir ~/data
```
데이터 디렉토리 안에 myid 파일을 생성한다.
```
> vi ~/data/myid
```
myid 파일 안에는 서버의 id에 해당하는 숫자만 적혀있으면 된다.
### 3.4 : Modify configuration file
설정파일을 수정한다.
```
> vi ~/src/kafka/config/server.properties
```
아래의 내용을 찾아 수정한다.
```
// 서버 data/myid의 값으로 세팅
broker.id=1
// 카프카의 메시지가 저장되는 디렉토리
log.dirs=/home/capstonegcp/data
// 주키퍼와의 연결 설정
// 서버호스트:서버포트/znode명
zookeeper.connect=zookeeper1:2181/kafka1
```
----------
## 4. Zookeeper
### 4.1 : Specify the host name
3.1 과 같은 내용을 수행한다.
### 4.2 : Download the code
Zookeeper 압축파일을 다운로드 받아 압축을 해제한다.
```
> cd ~/apps
> wget wget http://apache.mirror.cdnetworks.com/zookeeper/zookeeper-3.6.1/apache-zookeeper-3.6.1-bin.tar.gz
> tar -xvf apache-zookeeper-3.6.1-bin.tar.gz
```
압축해제한 Zookeeper 파일을 디렉토리 이동 후 심볼릭 링크를 설정한다.
```
> mv apache-zookeeper-3.6.1-bin ~/src
> cd ~/src
> ln -s apache-zookeeper-3.6.1-bin/ zookeeper
```
### 4.3 : Make data file
데이터 파일을 생성한다. 파일 안에는 주키퍼의 상태, 스냅샷 등의 정보가 저장된다.
```
> mkdir ~/data
```
Kafka와 마찬가지로 데이터 파일 안에 myid 파일을 생성한다.
```
> vi ~/data/myid
```
### 4.4 : Modify configuration file
설정파일을 생성한다. zookeeper/conf 안의 zoo_sample.cfg 내용을 복사해 사용한다.
```
> cd ~/src/zookeeper/conf
> cp zoo_sample.cfg zoo.cfg
> vi zoo.cfg
```
dataDir의 경로를 수정한다. 이 경로는 4.3 에서 만든 데이터 파일의 경로와 일치해야 한다.
```
dataDir=/tmp/zookeeper
-> dataDir=/home/capstonegcp/data
```
Zookeeper가 앙상블을 이루기 위한 서버의 정보를 추가한다. 여기서 2888은 동기화를 위한 포트, 3888은 클러스터 구성 시 리더를 선출하기 위한 포트이다.
```
server.1=zookeeper1:2888:3888
```
----------