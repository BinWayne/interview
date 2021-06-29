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

1. 当broker master 接收到消息后，尚未通知到其他副本broker 即通知，这种效率最高，但是也存在问题，有可能因为网络原因，后续没有吧消息同步到所有副本,默认 acks=1
2. 当所有broker节点收到消息后，在通知producer，这种保证消息一定都同步到了所有节点，但是性能较差`acks = all`
3. 可设置一部分副本收到消息后返回，例如设置3个 `replication.factor >= 3`

##### 消费端如何保证不丢失（不保证重复消费）

![tcpip](https://github.com/BinWayne/interview/blob/main/media/kafka_consumer.png)

kafka的消费端是根据偏移量来计算消费端的消费情况，一个consumer A 先自动提交offset 然后处理消息进行消费；这样的好处是 如果一个消息需要消费的时间特别长，等消费完了再提交offset 效率就很低；但如果先提交offset也会遇到问题，如果自动提交完offset，此时服务器挂了，其实消费者还未来得及消费；

所以应该吧自动提交offset改成手动提交，等消息消费完在手动提交offset；同样也会存在问题，当消息消费完之后，突然宕机，等恢复后 发现offset还在原始位置，此时又会出发重复消费。

##### 消息的重复消费

上一个消费方如何解决不丢失问题里，会有一种情况出现重复消费，重复消费的问题 本质就是如何保证幂等性；幂等性的方案就是保证全局唯一主键；可以利用数据库唯一id 或是利用全局redis 唯一key，在消费消息前时，先去redis里查下这个消息key 是否存在，如果存在代表之前宕机前已经消费过，如果不存在则可继续消费


