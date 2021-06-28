### Kafka学习

##### 为什么要用kafka？

1. 高性能
2. 低延迟
3. 高可扩展
4. 高可靠 （ zookeeper 机制）
5. 低延迟

##### kafka 核心概念

![tcpip](https://github.com/BinWayne/interview/blob/main/media/kafka_cluster.png)

**Producer**： 消息发送方
**Broker**: 相当于一个kafka运行示例
**Topic**： 消息集合，相当于数据库中的一张表
**partition**：分区，类似队列。一个topic下面可以新建多个分区，同一个分区里的消息一定是顺序排列。如果是多个分区里的消息 ，就没法保证顺序
**consumer**： 消费方，kafka默认使用pull 模型
**consumer group**：消费组，同一个消费组里可以有多个消费方，一个消费组和topic 绑定之后，消费组里的消费方都能收到该消息


