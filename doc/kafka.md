### Kafka学习

##### 为什么要用kafka？

1. 高性能
2. 低延迟
3. 高可扩展
4. 高可靠 （ zookeeper 机制）
5. 低延迟

##### kafka 核心概念

![tcpip](https://github.com/BinWayne/interview/blob/main/media/kafka_cluster.png)

1. **Producer**： 消息发送方
2. **Broker**: 相当于一个kafka运行示例
3. **Topic**： 消息集合，相当于数据库中的一张表
4. **partition**：分区，类似队列。一个topic下面可以新建多个分区，同一个分区里的消息一定是顺序排列。如果是多个分区里的消息 ，就没法保证顺序
5. **consumer**： 消费方，kafka默认使用pull 模型
6. **consumer group**：消费组，同一个消费组里可以有多个消费方，一个消费组和topic 绑定之后，消费组里的消费方都能收到该消息

##### kafka 如何解决消息不丢失？

消息经过发送方，broker，以及消费方最终消费。<br>
发送方产生消息，往broker发送消息，当broker 接收到消息后，会通知发送方收到消息，保证发送方的消息已经在broker端落盘写入磁盘<br>

生产broker 一般以集群模式提供服务，有三种情况反馈接收到消息

1. 当broker master 接收到消息后，尚未通知到其他副本broker 即通知，这种效率最高，但是也存在问题，有可能因为网络原因，后续没有吧消息同步到所有副本
2. 当所有broker节点收到消息后，在通知producer，这种保证消息一定都同步到了所有节点，但是性能较差
3. 可设置一部分副本收到消息后返回，例如设置3个




