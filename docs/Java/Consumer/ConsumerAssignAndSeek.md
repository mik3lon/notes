### Kafka consumer: Assign and seek 

In this case, we want to read from specific offsets in a topic partition, so we have:

```java
            String topic = "first_topic";
            TopicPartition partitionToReadFrom = new TopicPartition(topic, 0);
            long offsetToReadForm = 15L;
            consumer.assign(Arrays.asList(partitionToReadFrom));
    
            consumer.seek(partitionToReadFrom, offsetToReadForm);
    
            int numberOfMessageToRead = 5;
            boolean keepOnReading = true;
            int numberOfMessagesReadSoFar = 0;
    
            while (keepOnReading) {
                ConsumerRecords<String, String> records = consumer.poll(Duration.ofMillis(100));
    
                for (ConsumerRecord<String, String> record: records) {
                    numberOfMessagesReadSoFar += 1;
                    logger.info("Key: " + record.key());
                    logger.info("Value: " + record.value());
                    logger.info("Partition: " + record.partition());
                    logger.info("Offset: " + record.offset());
                    if (numberOfMessagesReadSoFar >= numberOfMessageToRead) {
                        keepOnReading = false;
                        break;
                    }
                }
            }
    
            logger.info("Exiting the application");
```

In this case we define that we want to read 5 messages of the partition 0 from the `first_topic` starting in the
offset 15.

A complete example is in this [link](https://github.com/mik3lon/kafka-course/blob/master/kafka-basics/src/main/java/github/mikelon/kafka/ConsumerDemoAssignSeek.java).