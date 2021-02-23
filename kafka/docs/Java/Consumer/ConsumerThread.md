### Kafka consumer in Java

In this case, we use a class that implements `Runnable` to get this characteristic. The class could be like:

```java
    public class ConsumerRunnable implements Runnable {
        Logger logger = LoggerFactory.getLogger(ConsumerRunnable.class.getName());

        private final CountDownLatch latch;
        private final KafkaConsumer<String, String> consumer;

        public ConsumerRunnable(
                String bootstrapServers,
                String groupId,
                String topic,
                CountDownLatch latch
        ) {
            this.latch = latch;

            Properties properties = new Properties();
            properties.setProperty(ConsumerConfig.BOOTSTRAP_SERVERS_CONFIG, bootstrapServers);
            properties.setProperty(ConsumerConfig.KEY_DESERIALIZER_CLASS_CONFIG, StringDeserializer.class.getName());
            properties.setProperty(ConsumerConfig.VALUE_DESERIALIZER_CLASS_CONFIG, StringDeserializer.class.getName());
            properties.setProperty(ConsumerConfig.GROUP_ID_CONFIG, groupId);
            properties.setProperty(ConsumerConfig.AUTO_OFFSET_RESET_CONFIG, "earliest");

            this.consumer = new KafkaConsumer<String, String>(properties);
            this.consumer.subscribe(Collections.singletonList(topic));
        }

        @Override
        public void run() {
            try {
                while (true) {
                    ConsumerRecords<String, String> records = this.consumer.poll(Duration.ofMillis(100));

                    for (ConsumerRecord<String, String> record: records) {
                        logger.info("Key: " + record.key());
                        logger.info("Value: " + record.value());
                        logger.info("Partition: " + record.partition());
                        logger.info("Offset: " + record.offset());
                    }
                }
            } catch (WakeupException e) {
                logger.info("Received shutdown signal!");
            } finally {
                this.consumer.close();

                // Tell out main code we're done
                latch.countDown();
            }
        }

        public void shutdown() {
            // Special method to interrupt consumer.poll
            // It will throw the exception WakeUpException
            this.consumer.wakeup();
        }
    }
```

A complete example is in this [link](https://github.com/mik3lon/kafka-course/blob/master/kafka-basics/src/main/java/github/mikelon/kafka/ConsumerDemoWithThread.java).