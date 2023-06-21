2022/3/6

# 集线器Hub、交换机Switch、路由器Router区别

rongtianfu@gmail.com

## 原网站

[集线器Hub，交换机Switch，路由器Router区别 - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/346426970)

## 全文

### 一、集线器Hub

集线器的目的是在其**内部将所有的网络连通**，它是一个具有多个端口的设备，**用于网络设备的互连**。集线器不过滤任何数据，也不知道数据要发送到什么地方，集线器唯一知道的: 当数据到达tade一个端口时，集线器会复制数据包到它所有端口，这样，连接到该集线器上的所有设备都可以收到数据包。**当数据包进入集线器的某个端口时，它将被集线器重新广播到其他所有端口**。if这台计算机与另外某台计算机通信，内部网络中的其他计算机也会收到这些数据，即使这些数据不是要发给它们的。会在网络上造成不必要的流量，浪费带宽（waste bandwidth）。



### 二、交换机Switch

switch和集线器非常相似，它也是一个具有多个端口、用于网络设备互联的设备，但是**交换机可以学习连接到target的物理地址，**switch**将这些称为MAC地址的物理地址存储在自己的地址表中。**

**当数据包发送到**switch**时，数据包会被直接发送到预期的目的端口，而不是像集线器那样，只是将数据包重新广播到每个端口。**

举个例子，如果这台计算机想要和另外一台计算机通信，数据包到达switch后，switch在自己的地址表中查看与数据包携带的目的MAC地址匹配的端口，然后将数据包传送到该端口，数据包就只会发送到想要与之通信的那台计算机。**可以减少网络上不必要的流量**。

HUB only detects that a device is physically connected to it, SWITCH can detect specific devices that are connected to it, keeps a record of the MAC addresses of those devices.

**Hub和Switch用于在本地区域内交换数据**，例如在家庭网络中，它们不能在外部网络上（如internet上）交换数据。

**要将数据在自己网络之外交换/路由到另一个网络，例如internet，设备需要能够读取IP address**，而hub和switch不能读取IP address，这就**需要用到router。**



### 三、路由器Router

router是**根据IP address，将一个数据包从一个网络路由/转发到另一个网络的设备**.

当router接受到数据包时，router会检查数据包的IP address，并确定该数据包是要发送给自己所在的网络，还是要发送给其他网络.

如果router确定数据包是发送给自己所在的网络，就接受它；如果数据包不是发送给自己所在的网络，router就将这些数据包转发给其他网络.

router**本质上是一个网络的网关(The router is the gateway of a network)**。



### Summary:

**Hub & Switch are used to create networks, Router is used to connect networks**