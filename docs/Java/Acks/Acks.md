# Producer acknowledgment

We have basically 3 options to configure `acks` Producer property.

### Acks = 0
![](acks_0.png)

### Acks = 1
![](acks_1.png)

### Acks = all
![](acks_all.png)
![](acks_all_in_sync_replicas.png)

### Example:
If we use min.insync.replicas=2 and 2 brokers goes down, we have the next situation:
![](acks_all_exception.png)


For the video explication follow this [link](https://subscription.packtpub.com/video/application_development/9781789342604/99134/99140/acks-and-min-insync-replicas).


