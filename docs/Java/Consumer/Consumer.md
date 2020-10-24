### Kafka consumer in Java

The steps to create a consumer are the following:

* Create consumer properties:

```java
        String bootstrapServers = "127.0.0.1:9092";
        String groupId = "my-fourth-application";
        
        Properties properties = new Properties();
        properties.setProperty(ConsumerConfig.BOOTSTRAP_SERVERS_CONFIG, bootstrapServers);
        properties.setProperty(ConsumerConfig.KEY_DESERIALIZER_CLASS_CONFIG, StringDeserializer.class.getName());
        properties.setProperty(ConsumerConfig.VALUE_DESERIALIZER_CLASS_CONFIG, StringDeserializer.class.getName());
        properties.setProperty(ConsumerConfig.GROUP_ID_CONFIG, groupId);
        properties.setProperty(ConsumerConfig.AUTO_OFFSET_RESET_CONFIG, "earliest");
```

In this case, we use `group.id` config to set the application name (consumer-group).

* Instantiate the Consumer and subscribe to topic

```java
        String topic = "first_topic";
        KafkaConsumer<String, String> consumer = new KafkaConsumer<String, String>(properties);

        // subscribe consumer to out topic(s)
        consumer.subscribe(Collections.singletonList(topic));
```

* Read data from topic:
```java
        while (true) {
            ConsumerRecords<String, String> records = consumer.poll(Duration.ofMillis(100));

            for (ConsumerRecord<String, String> record: records) {
                logger.info("Key: " + record.key());
                logger.info("Value: " + record.value());
                logger.info("Partition: " + record.partition());
                logger.info("Offset: " + record.offset());
            }
        }
```

A complete example is in this [link](https://github.com/mik3lon/kafka-course/blob/master/kafka-basics/src/main/java/github/mikelon/kafka/ConsumerDemo.java).