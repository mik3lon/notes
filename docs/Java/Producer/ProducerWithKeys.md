### Kafka producer with keys in Java

In this case, we have to use another producer method:

```java
    for(int i= 0; i<10; i++ ) {
            String value = "hello world " + i;
            String key = "id_" + i;
            ProducerRecord<String, String> record =
                    new ProducerRecord<String, String>(topic, key, value);

            logger.info("key : " + key);

            // send data
            producer.send(record, (recordMetadata, e) -> {
                // execute every time a record is successfully or an exception is thrown
                if (e == null) {
                    logger.info(
                            "Received new metadata: \n"
                                    + "Topic: " + recordMetadata.topic() + "\n"
                                    + "Partition: " + recordMetadata.partition() + "\n"
                                    + "Offset: " + recordMetadata.offset() + "\n"
                                    + "TimeStamp: " + recordMetadata.timestamp()
                    );
                } else {
                    logger.error("Error while producing: " + e);
                }
            }).get();
        }
```


As we can see `new ProducerRecord<String, String>(topic, key, value);` in this case, we need three parameters.

Complete example in this [link](https://github.com/mik3lon/kafka-course/blob/master/kafka-basics/src/main/java/github/mikelon/kafka/ProducerDemoKeys.java)