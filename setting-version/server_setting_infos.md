# Server Setting Infos

| Server                   | Installs                                         | GCP ports to allow                                  |
| ------------------------ | ------------------------------------------------ | --------------------------------------------------- |
| All Servers              | wget <br> Java <br> Docker <br> (images) Jenkins | tcp/8181 and tcp/50000 for Jenkins                  |
| Producer Server          | Maven                                            | tcp/9990 for Netty server                           |
| Kafka & Zookeeper Server | (images) Kafka + Zookeeper                       | tcp/9092 for Kafka cluster                          |
| Consumer Server          | Maven <br> (images) Elasticsearch + Kibana       | tcp/9200 for Elasticsearch <br> tcp/5601 for Kibana |

-   Reserve an GCP external IP to allow accesses from customers or users.
