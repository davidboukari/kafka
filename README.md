# kafka

* https://blog.zenika.com/2021/04/07/lavenir-de-zookeeper-dans-une-architecture-kafka/
<img width="664" alt="image" src="https://user-images.githubusercontent.com/32338685/138103525-602a751b-bd18-48fa-94d4-e271df5a1722.png">


## Sources 

* https://openclassrooms.com/fr/courses/4451251-gerez-des-flux-de-donnees-temps-reel/4451521-metamorphosez-vos-applications-temps-reel-avec-kafka
* https://downloads.apache.org/kafka/2.4.1/kafka_2.11-2.4.1.tgz

## Python

* [python sample](pythonsample.md)

## Basic configuration


### Start the cluster manager zookeeper

```bash
./bin/zookeeper-server-start.sh ./config/zookeeper.properties

cat ./config/zookeeper.properties

dataDir=/tmp/zookeeper
clientPort=2181
maxClientCnxns=0

```



### Start the cluster Broker


```bash
./bin/kafka-server-start.sh ./config/server.properties

cat ./config/server.properties

# Identifiant de notre broker
broker.id=0
# Nom d'hôte et port sur lequel écoute le broker Kafka
listeners=PLAINTEXT://:9092
# Décommentez cette ligne pour permettre la suppression de topic, ce qui
# sera utile par la suite
delete.topic.enable=true
# Vérifiez que vous disposez de suffisamment d'espace disque sur la
# partition qui contient ce répertoire
log.dirs=/tmp/kafka-logs
num.partitions=1
# Paramètres concernant la rétention des données
log.retention.hours=168
log.segment.bytes=1073741824
log.retention.check.interval.ms=300000
# Connexion à Zookeeper
zookeeper.connect=localhost:2181
zookeeper.connection.timeout.ms=6000

```

### *Manage message: topics*

### Create a topics

```
./bin/kafka-topics.sh --create --zookeeper localhost:2181 --replication-factor 1 --partitions 1 --topic blabla
```

### List  topics

```bash
./bin/kafka-topics.sh --list --zookeeper localhost:2181

./bin/kafka-topics.sh --describe --zookeeper localhost:2181 --topic blabla
```


### Produce messages for topics

```bash
./bin/kafka-console-producer.sh --broker-list localhost:9092 --topic blabla

```

### Consum messages

```bash
./bin/kafka-console-consumer.sh --bootstrap-server localhost:9092 --topic blabla

./bin/kafka-console-consumer.sh --bootstrap-server localhost:9092 --topic blabla --consumer-property group.id=mygroup
```

### List consumers

```bash
 ./bin/kafka-consumer-groups.sh --bootstrap-server localhost:9092 --list
 
 ./bin/kafka-consumer-groups.sh --bootstrap-server localhost:9092 --describe --group mygroup
 ```
 
 
### Increase partitions

```bash
./bin/kafka-topics.sh --alter --zookeeper localhost:2181 --topic blabla --partitions 2
```




