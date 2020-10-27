# kafka-notes

All info about kafka.

- [CLI](docs/CLI.md)
- Java programming:
    * Producers:
        * [Simple producer](docs/Java/Producer/Producer.md) 
        * [With keys](docs/Java/Producer/ProducerWithKeys.md)
        * [With callback](docs/Java/Producer/ProducerWithCallback.md)
    * Consumers: 
        * [Simple consumer](docs/Java/Consumer/Consumer.md)
        * [Threaded consumer](docs/Java/Consumer/ConsumerThread.md)
        * [Assign and seek](docs/Java/Consumer/ConsumerAssignAndSeek.md)
    * Advanced Configurations:
        * Producer:
            * [Delivery](docs/Java/AdvancedConfigurations/Producer/Delivery/Acks.md)
            * [Retries](docs/Java/AdvancedConfigurations/Producer/Retries/Retries.md)
            * [Compression](docs/Java/AdvancedConfigurations/Producer/Compression/Compression.md)
            * [Linger and batch](docs/Java/AdvancedConfigurations/Producer/LingerBatch/LingerBatch.md)
            * [Partition and key hashing](docs/Java/AdvancedConfigurations/Producer/Partition/Partition.md)
            * [max.block.ms and buffer.memory](docs/Java/AdvancedConfigurations/Producer/MaxBlockAndBufferMemory/MaxBlockAndBufferMemory.md)
        * Consumer:
            * [Delivery semantics](docs/Java/AdvancedConfigurations/Consumer/Semantics/Semantics.md)
            * [Poll behaviour](docs/Java/AdvancedConfigurations/Consumer/PollBehaviour/PollBehaviour.md)
            * [Commit offsets strategies](docs/Java/AdvancedConfigurations/Consumer/CommitOffsetStrategies/CommitOffsetStrategies.md)
            * [Internal threads](docs/Java/AdvancedConfigurations/Consumer/InternalThreads/InternalThreads.md)
    * Real world insights
        * [Choosing partition count and replication factor](docs/RealWorldInsights/RealWorldInsights.md)
    * Advanced partition configurations
        * [Segments and Indexes](docs/AdvancedTopicsConfig/AdvancedTopicsConfig.md)