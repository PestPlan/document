# Server Setting Infos

| Server | Installs | GCP ports to allow |
| ------ | -------- | ------------------ |
| All Servers | wget <br> Java |  |
| Producer Server | Maven | tcp/9990 for Netty server |
| Kafka & Zookeeper Server | Docker <br> (images) Jenkins + Kafka + Zookeeper | tcp/9092 for Kafka cluster <br> tcp/8181 and tcp/50000 for Jenkins |
| Consumer Server | Maven <br> Docker <br> (images) Elasticsearch + Kibana | tcp/9200 for Elasticsearch |

* Reserve an GCP external IP to allow accesses from customers or users.