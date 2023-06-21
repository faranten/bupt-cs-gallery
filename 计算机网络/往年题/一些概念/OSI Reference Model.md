2022/3/7

# OSI and TCP/IP

rongtianfu@gmail.com

## OSI

### Physical layer

1. volts, 0 and 1
2. how many nanoseconds a bit lasts
3. 能否双向同时处理
4. 第一次连接如何建立，当连接完成的时候如何断开

### Data link layer

该层的关键是完成比特流和数据流之间的相互转换

1. 将高层数据转换成数据帧（在个别协议中，如果有必要）（大部分协议没有 break up 的操作）
2. confirm and acknowledgement
3. Flow control（CPU处理能力不足以处理到达的数据，对方发送数据太快）
4. 给出了如何在 broadcast networks 中如何共享信道 channel(s)

### Network layer

该层的主要涉及到 subnet，主要到功能是路由 routing 和转发 forwarding。该层主要是点到点 point-to-point 的结构（两台计算机之间必须通过某介质直接连接）

1. forwarding（重要功能）
2. routing，how packets are routed from source to destination，这通过路由表 router table 来实现，每个路由器单独判断（与沿途其他路由器无关）。下面给出路由表的生成方式：
   1. static，此时的路由表是固定不变的
   2. be determined at the start of each conversation，此时的路由表是在每次连接一开始生成的
   3. highly dynamic，此时的路由表是动态的、随着时间的推移而（自动）更新的
3. congestion 拥塞控制，通过协议实现，不能允许用户疯狂发送数据
4. QoS 质量控制，主要指标为延迟 delay、中转时间 transit time、抖动jitter，延迟和抖动一般比较重要，比如说，在语音通话中，我每 20ms 发送一个数据包，而如果抖动较大，则你那边数据包的间隔时间不稳定，则不能得到我准确的语音，在网络上看视频的时候，预先缓存一段时间就是为了缓解网络抖动
5. heterogeneous networks interconnection 异构网络互联，指的是不同网络的互联，后面的学习内容主要就是基于此
6. 在 broadcast network 中，routing 机制是简单的，因为根本不需要多么仔细地去 routing



**以上层次必须在 subnet 中完成**

### Transport layer

该层主要是端到端 end-to-end，这是一个更高层次的概念（两台计算机之间可能是极为复杂的网络），而 point-to-point 仅仅是针对同一个 subnet 中两个计算机而言的

1. 接收高层的数据，并在有必要的时候 split it up into smaller units
2. 决定给会话层提供的服务，主要有：
   1. an error-free end-to-end channel
   2. 传送单独的消息，而不保证它们的到达（发出去就不管了，理论上能到达，实际上不管）
   3. broadcasting of messages to multiple destinations，在data link layer 中，一般支持广播机制，此时直接用特定的地址字段完成组播的功能，而若某网络本身不支持广播机制（如果支持则直接用），那么需要一个一个发送
3. congestion control，大部分拥塞控制的功能通过传输层的协议实现，拥塞控制对互联网生存至关重要。通过传输层协议可以实现控制数据发送速度的功能（如果当前互联网拥塞程度大，则所有的计算机根据协议都将主动降低数据的发送速率，等到没问题时再缓慢调高）。网络拥塞时发送的数据包被丢掉

### Session layer

该层没那么重要，主要涉及到 different machines，此处的 machine 指的是虚拟机的概念，在同一计算机内亦可以造出两个虚拟机

1. dialog control
2. token management 令牌管理
3. synchronization 同步，涉及到同步点的概念（比如在下载东西的时候突然断网，下次联网的时候不必从头下载，而是从某个确定点开始下载）

### Presentation layer

1. 规定了合适的 syntax 语法和 semantics 语义确保数据的表示方法相同，比如一台机器是大端法、另一台机器是小端法，则它们在交换数据的时候需要定义一个共同的数据的表示方式

### Application layer

各种各样的网络应用



## TCP/IP

### Host-to-network layer

有时翻译成网络接口层，对应 physical layer and data link layer

### Internet layer

对应 network layer

1. A packet-switching network based on a connectionless internetwork layer
2. Defines an official packet format and protocol called IP (Internet Protocol)
3. The job of the internet layer is to deliver IP packets where they are supposed to go
   1. packet routing
   2. avoiding congestion

路由器有责任避免拥塞（路由器有一系列算法尽量避免拥塞）

### Transport layer

对应 transport layer

1. TCP：
   1. 可靠的、面向连接的字节流（如果有问题则重新发送）
   2. 对于发出去的数据，fragments incoming byte stream into discrete messages
   3. 对于接收到的数据，reassemble the received messages into the output stream
   4. 流量控制
   5. 字节流是没有边界的，需要更高层次的协议来处理。另外，TCP似乎也可以实现报文序列，这是有边界的
2. UDP：
   1. 不可靠的、无连接的数据报
   2. For applications that do not want TCP's sequencing or flow control and wish to provide their own
   3. For applications in which prompt delivery is more important than accurate delivery, such as transmitting speech or video, DNS
   4. 数据包是有边界的

### Application layer

对应 application layer，OSI 模型中的 presentation layer 和 session layer 在 TCP/IP 模型中没有对应的