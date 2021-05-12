# Server Setting Infos

| Server                   | Installs                                         | GCP ports to allow                                  |
| ------------------------ | ------------------------------------------------ | --------------------------------------------------- |
| All Servers              | wget <br> Java <br> Docker <br> (images) Jenkins | tcp/8181 and tcp/50000 for Jenkins                  |
| Producer Server          | Maven                                            | tcp/9990 for Netty server                           |
| Kafka & Zookeeper Server | (images) Kafka + Zookeeper                       | tcp/9092 for Kafka cluster                          |
| Consumer Server          | Maven <br> Python       | tcp/27017 for MongoDB |
| Database Server          | MariaDB <br> MongoDB       |  tcp/3306 for MariaDB <br> tcp/17017 for MongoDB|

-   Reserve an GCP external IP to allow accesses from customers or users.
