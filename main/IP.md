# IP

## IPv4

由32位二进制数组成，常以xxx.xxx.xxx.xxx形式表现（xxx为小于等于255的十进制数字）。分为ABCDE五大类。

> D类多播,E类实验,都不能直接分配给计算机, 所以一般只讨论ABC

|                            | A类IPv4地址             | B类IPv4地址               | C类IPv4地址                 |
| -------------------------- | ----------------------- | ------------------------- | --------------------------- |
| **最大主机数(每个网络)** | 16777214 (2^24-2)       | 65534 (2^16-2)            | 254 (2^8-2)                 |
| IP地址范围                 | 1.0.0.0~127.255.255.255 | 128.0.0.0~191.255.255.255 | 192.0.0.0~223.255.255.255   |
| 私有IP地址范围             | 10.0.0.0~10.255.255.255 | 172.16.0.0~172.16.255.255 | 192.168.0.0~192.168.255.255 |
| 网络数量                 | 126 (2^7-2)             | 16384 (2^14)              | 2097152 (2^21)              |
| 可用IP地址范围             | 1.0.0.1~127.255.255.254 | 128.0.0.1~191.255.255.254 | 192.0.0.1~223.255.255.254   |
| 网络标志位                 | 0                       | 10                        | 110                         |
| 适用范围                   | 大量主机的大型网络      | 中等规模主机数的网络      | 小型局域网                  |

> 计算IP地址数时减2，是因为地址不能全0或全1

## 子网掩码

IP & netmask来确定子网，ABC类的具体实现。  
如192.168.23.35 & 255.255.255.0 = 192.168.23.0。即2^8-2=254，网络ID为192.168.23，广播地址192.168.23.255，需要内网中包含200左右的物理机适用。

## CIDR Classless Inter-Domain Routing 无类型域间选路

IP地址/网络ID的位数，消除ABC类的概念，比掩码更精细地分配子网。  
如192.168.23.35/11，其中用11表示网络ID。即2^11-2=2046，需要内网中包含2000左右的物理机适用。

> 相同网络ID即相同子网，通讯不需要路由器，查找MAC即可。
> 家庭常见网络ID 192.168.0，网关192.168.0.1。属C类netmask: 255.255.255.0 或 CIDR: /24
> 192.168.23.35/22 形如这种CIDR不是8的倍数，需要换算成二进制去求其子网的第一个地址、子网掩码、广播地址。不过不常用。

## ifconfig

```ifconfig
en0: flags=8863<UP,BROADCAST,SMART,RUNNING,SIMPLEX,MULTICAST> mtu 1500
    options=400<CHANNEL_IO>
    ether dc:a9:04:8f:98:4b
    inet 192.168.1.4 netmask 0xffffff00 broadcast 192.168.1.255
    media: autoselect
    status: active
```

- ether MAC地址
- inet IP地址
- netmask 子网掩码
- broadcast 广播地址
- net_device flags 网络设备的状态标识
  - BROADCAST 该网卡有广播地址
  - MULTICAST 网卡可以发送多播包
  - UP 网卡运行中
  - LOWER_UP 网卡L1运行中，即L1插着网线
- mtu 网卡网络包(MAC头+正文)最大传输1500字节（默认值）
- qdisc 内核发送数据包的排队规则 queueing discipline。
  - pfifo 先入先出
  - pfifo_fast 分三个带有优先级波段（band）分别先入先出。
  - noqueue 无队列

## ref

[1](https://blog.csdn.net/yexiangCSDN/article/details/85259714)