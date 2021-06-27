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
