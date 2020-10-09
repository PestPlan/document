## 1. Jenkins
Docker Hub 에서 Jenkins 이미지를 설치한다. 최근 버전 사용을 위해 lts 로 설치한다.
```
> sudo docker pull jenkins/jenkins:lts
```
설치된 이미지는 아래 명령어를 통해 확인할 수 있다.
```
> sudo docker images
```
Jenkins 이미지를 실행한다.
```
> sudo docker run -d -p 8181:8080 -p 50000:50000 -v jenkins_home:/var/jenkins_home --name jc_jenkins -u root jenkins/jenkins:lts
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
> sudo docker ps  // 실행 중이지 않은 컨테이너 목록까지 보고싶다면 -a 옵션을 추가한다.
```
----------
## 2. Elasticsearch
Docker Hub 에서 Elasticsearch 7.9.2. 버전을 설치한다.
```
> docker pull docker.elastic.co/elasticsearch/elasticsearch:7.9.2
```
Elasticsearch 이미지를 single-node 로 실행한다.
```
> docker run -p 9200:9200 -p 9300:9300 -e "discovery.type=single-node" docker.elastic.co/elasticsearch/elasticsearch:7.9.2
```