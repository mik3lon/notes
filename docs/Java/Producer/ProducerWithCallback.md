### Kafka producer with keys in Java

In this case, we use the second parameter of the `send` method to define a callback in order to perform
some actions according the status of the dispatch. 

```java
        for(int i= 0; i<10; i++ ) {
            ProducerRecord<String, String> record =
                    new ProducerRecord<String, String>(topic, "Hello world " + i);

            // send data
            producer.send(record, new Callback() {
                @Override
                public void onCompletion(RecordMetadata recordMetadata, Exception e) {
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
                }
            });
        }
```


Complete example in this [link](https://github.com/mik3lon/kafka-course/blob/master/kafka-basics/src/main/java/github/mikelon/kafka/ProducerWithCallbackDemo.java)