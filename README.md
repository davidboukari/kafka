# kafka

## Sources 

* https://data-flair.training/blogs/kafka-architecture/
* http://kafka.apache.org/
* https://downloads.apache.org/kafka/2.4.1/kafka_2.12-2.4.1.tgz



## Basic configuration

### For kafka1

* broker.id=1
* listeners=PLAINTEXT://:9091
* zookeeper.connect=localhost:2181,localhost:2182
* log.dirs=/home/vagrant/kafka1/logs

### For kafka2

* broker.id=2
* listeners=PLAINTEXT://:9092
* zookeeper.connect=localhost:2181,localhost:2182
* log.dirs=/home/vagrant/kafka2/logs


```bash
./bin/kafka-topics.sh --create --zookeeper localhost:2181 --replication-factor 3 --partitions 50 --topic demo
```
