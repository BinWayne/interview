# 面试题

#### TCP 如何保证可靠性？ 简述 TCP建立连接和断开的过程？

TCP 是通过下面几个特性保证数据传输的可靠性：

* 序列号和确认应答信号
* 超时重发控制
* 连接管理
* 滑动窗口控制
* 流量控制
* 拥塞控制
  
  有问必有答 = 确认机制；如果没反应，发送端会认为发送失败，会重发。
  ![tcpip](https://github.com/BinWayne/interview/blob/main/media/tcp.png)
  
  主要通过3次握手协议和超时重发控制
  
  ##### 如何通过3次握手协议控制？
  
  ![tcpip](https://github.com/BinWayne/interview/blob/main/media/3times.png)
  四个概念需要谨记：
  
  **Sequence Number**是包的序号，**用来解决网络包乱序（reordering）问题。**
  **Acknowledgement Number**就是ACK——用于确认收到，**用来解决不丢包的问题**。
  **Window又叫Advertised-Window**，也就是著名的滑动窗口（Sliding Window），**用于解决流控的**。
  **TCP Flag** ，也就是包的类型，**主要是用于操控TCP的状态机的**。
  
  TCP状态机：
  其实两个服务器之间所谓的**连接** 是双方各自维护一个TCP状态，用于知晓对方的TCP状态。
  
  ##### 3次连接过程：
* 服务端必须准备接收传入的连接。这通常通过调用`socket`，`bind`和`listen`来完成，称为被动打开。
* 客户端通过调用`connect`方法来发起一个主动的打开。客户端TCP会发送一个“同步”(SYN)段，它告诉服务器客户端在连接上发送的数据的初始序列号。通常情况下，SYN没有发送数据，它只包含一个IP头，TCP头和可能的TCP选项。
* 服务器必须确认（ACK）客户端的SYN，并且服务器还必须发送自己的SYN，其中包含服务器将在连接上发送的数据的初始序列号。
* 客户端必须确认服务器的SYN。

为什么会有最后一个客户端确认？
因为有可能server端向client发送确认消息后，client迟迟无法收到，此时如果server端向client端发送消息，client可能网络原因是真的没法收到消息。




