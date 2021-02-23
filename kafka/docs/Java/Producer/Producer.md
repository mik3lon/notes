### Kafka producer in Java

In order to produce data into a kafka topic, we will use the KafkaProducer class. First of all, we have to 
add to `pom.xml` the kafka-client [dependency](https://mvnrepository.com/artifact/org.apache.kafka/kafka-clients):

```xml
    <dependency>
        <groupId>org.apache.kafka</groupId>
        <artifactId>kafka-clients</artifactId>
        <version>2.6.0</version>
    </dependency>
```

The steps to create produce data into kafka are the following:

* Create producer properties:

```java
Properties properties = new Properties();

properties.setProperty(ProducerConfig.BOOTSTRAP_SERVERS_CONFIG, boostrapServers);
properties.setProperty(ProducerConfig.KEY_SERIALIZER_CLASS_CONFIG, StringSerializer.class.getName());
properties.setProperty(ProducerConfig.VALUE_SERIALIZER_CLASS_CONFIG, StringSerializer.class.getName());
```

* Instantiate the Producer:

```java
KafkaProducer<String, String> producer = new KafkaProducer<String, String>(properties);
```

* Produce and send data:
```java
ProducerRecord<String, String> record =
        new ProducerRecord<String, String>(topic, "Hello world! from my Java App!");

producer.send(record);
producer.flush();
producer.close();
```

By default, the producer is async, so we have to call flush in order to perform the action.

A complete example is in this [link](https://github.com/mik3lon/kafka-course/blob/master/kafka-basics/src/main/java/github/mikelon/kafka/ProducerDemo.java).