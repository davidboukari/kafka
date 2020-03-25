# kafka

## Sources 

* https://openclassrooms.com/fr/courses/4451251-gerez-des-flux-de-donnees-temps-reel/4451521-metamorphosez-vos-applications-temps-reel-avec-kafka
* https://data-flair.training/blogs/kafka-architecture/
* http://kafka.apache.org/
* https://downloads.apache.org/kafka/2.4.1/kafka_2.12-2.4.1.tgz



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

### Manage message: topics

Create a topics

```
./bin/kafka-topics.sh --create --zookeeper localhost:2181 --replication-factor 1 --partitions 1 --topic blabla
```

List  topics

```bash
./bin/kafka-topics.sh --list --zookeeper localhost:2181

./bin/kafka-topics.sh --describe --zookeeper localhost:2181 --topic blabla
```


### Produce messages

```bash
./bin/kafka-console-producer.sh --broker-list localhost:9092 --topic blabla

```

### Read messages

```bash
./bin/kafka-console-consumer.sh --bootstrap-server localhost:9092 --topic blabla
```








