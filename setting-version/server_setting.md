# Server Setting Info

## 0. Preinstall
* wget
* Java

## 1. Producer Server
### Install
* Maven

### GCP settings
* Reserve an external IP to access from customers or users.   
* Allow firewall on port tcp/9990 to connect to Netty Server.

## 2. Kafka Server
### Installl
* Kafka

### GCP settings
* Reserve an external IP to access from customers or users.   
* Allow firewall on port tcp/9092 to connect to Kafka cluster.

## 3. Zookeeper Server
### Install
* Zookeeper

### GCP settings
* Reserve an external IP to access from customers or users.   
* Allow firewall on port tcp/2181 to connect to Zookeeper.

## 4. Consumer Serer
### Install
* Maven