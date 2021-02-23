# Producer compression

We can use compression in order to get more throughput and low latency when producing messages to Kafka. 

![](compression.png)

This is the compression flow:

![](compression_process.png)

Compression provide us some advantages:

![](compression_advantages.png)

Recommendations are:

![](compression_recommendations.png)


Next, we have a look at the implementation. So we must set these properties in our property class:

```java
properties.setProperty(ProducerConfig.COMPRESSION_TYPE_CONFIG, "snappy");
```



