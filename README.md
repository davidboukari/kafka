# kafka

## Sources 

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

### Start the cluster server

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










