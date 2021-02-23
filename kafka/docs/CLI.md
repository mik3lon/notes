## Kafka CLI

#### Start zookeeper
```shell script
bin/zookeeper-server-start.sh config/zookeeper.properties
```
#### Start Kafka
```shell script
bin/kafka-server-start.sh config/server.properties
```
 
 
#### Kafka topics commands
* Create topic:
```shell script
bin/kafka-topics.sh --create --topic twitter_tweets --partitions 6 --zookeeper 127.0.0.1:2181 --replication-factor 1
```

* List topics:
```shell script
bin/kafka-topics.sh --zookeeper 127.0.0.1:2181 --list
```

* Describe a topic:
```shell script
bin/kafka-topics.sh --zookeeper 127.0.0.1:2181 --topic twitter_tweets --describe
```

* Delete a topic:
```shell script
bin/kafka-topics.sh --zookeeper 127.0.0.1:2181 --topic test --delete
```
 
#### Kafka Console producer commands
* Producer to topic:
```shell script
bin/kafka-console-producer.sh --topic first_topic --bootstrap-server localhost:9092
```
* Producer to topic with properties:
```shell script
bin/kafka-console-producer.sh --topic first_topic --bootstrap-server localhost:9092 --producer-property acks=all
```

If the topic does not exist, it will be created (with default values -> server.properties)

#### Kafka Console consumer commands

* Consumer from topic:
```shell script
bin/kafka-console-consumer.sh --topic first_topic --bootstrap-server localhost:9092 --from-beginning
```
#### Consumer groups commands
* Consumer group:
```shell script
bin/kafka-console-consumer.sh --topic first_topic --bootstrap-server localhost:9092 --from-beginning --group my-first-application
```
* List consumer groups:
```shell script
bin/kafka-consumer-groups.sh --bootstrap-server 127.0.0.1:9092 --list
```
* Describe a consumer group:
```shell script
bin/kafka-consumer-groups.sh --bootstrap-server 127.0.0.1:9092 --describe --group my-first-application
```
* Reset offset:
```shell script
bin/kafka-consumer-groups.sh --reset-offsets --to-earliest --bootstrap-server 127.0.0.1:9092 --group my-first-application --execute --topic f
irst_topic
```
* Shift by 2 offset:
```shell script
bin/kafka-consumer-groups.sh --reset-offsets --shift-by -2 --bootstrap-server 127.0.0.1:9092 --group my-first-application --execute --topic first_topic
```
