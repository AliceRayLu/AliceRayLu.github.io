---
title: 计算机网络(22Fall)
date: 2023-02-26
category: [Knowledge, Computer Network]
---

# 计算机网络（2022）

非上课笔记版，课后复习整理重点版

名词解释重点标出

## 网络基本知识

### 网络分类

* 广域网（WAN-wide area network）
* 城域网（MAN）
* 局域网（LAN-local area network）
* 个人区域网（PAN）

### 网络设备

* **交换机**(switch)【划分冲突域，不能阻断广播域】

  多端口网桥，交换机使用硬件转发

  通过reduce traffic和increase bandwidth缓解拥塞
* **集线器**(hub)【有多个端口，发给所有端口】

  重新生成，重定时网络信号
* **中继器**(repeater)【只有2个端口，一端口入，另一端口出】

  延长网络：整理、放大、重发信号（不划分冲突）
* **网桥**(bridge)【划分冲突域】

  过滤信息，有一张mac表决定转发到不同网段，收集并在段之间传递数据包

  网桥使用软件包转发
* [路由器(router)](siyuan://blocks/20221124204504-5ry1owq)【划分冲突域，阻断广播域】

  流量调节，网段划分，选择最佳报文转发路径
* **网卡**(NIC)

  拥有mac地址（**物理地址，48位**），用于控制网络上主机的数据通信

  封装帧&识别帧（第二层），帮助主机接入网络，发送接收比特信号（第一层）

【网络设备划分】

* 按照作用范围划分

  * 局域网设备：hub, bridge, switch, router, NIC
  * 广域网设备：router, modem
* 按照OSI模型划分

  * 第一层：hub, repeater, NIC
  * 第二层：bridge, switch, NIC
  * 第三层：router

### **名词解释收集**

* ISP：internet service provider, 网络服务供应商

  WISP: wireless internet service provider
* NAP：network access point, 网络接入点
* DTE：数据终端设备，Data Terminal Equipment

  DCE：数据通信设备/数据回路终端，Data Circuit-terminating Equipment
* Mbps: 一秒传输几百万比特
* OSI：open systems interconnection
* **RFC**：request for comment请求评论，包含关于Internet所有重要文件文字资料，包括大量网络标准
* [EMI](siyuan://blocks/20221124210409-1gt0foc)：电磁干扰（Electro-Magnetic Interference）
* [RFI](siyuan://blocks/20221124210409-1gt0foc)：射频干扰（Radio Frequency Interference）
* [ILD](siyuan://blocks/20230106152938-cn05bhp)：注入式激光二极管 (injection laser diode)
* LED：发光二极管（light-emitting diode）
* IEEE：Institute of Electrical and Electronics Engineers，美国电气和电子工程师协会

  UL—Underwriters Laboratories美国保险商安全标准

  EIA—Electronic Industries Alliance电子工业协会

  TIA—Telecommunications Industry Association美国通信工业协会

  ANSI—American National Standards Institute美国国家标准学会

  [ARIN](siyuan://blocks/20230204162625-e3jy4wu)：american registry for internet numbers

  ISO：international standardization organization
* [NRZ](siyuan://blocks/20230126162401-lrtfz85)：不归零制码

  RZ：归零制码

  AMI：双极性传号交替反转码
* [多路复用技术](siyuan://blocks/20230126170209-rb1bda4)

  * TDM：time division multiplexing时分复用
  * FDM：frequency division multiplexing频分复用
  * WDM：wavelength division multipexing波分复用
  * CDM：code division multiplexing码分复用/CDMA：code division multiple access码分多址，各个用户使用不同码型
* [LLC](siyuan://blocks/20230129141636-z556cqj)：logical link control逻辑信号控制

  [MAC](siyuan://blocks/20221124210953-p4the2e)：media access control介质接入控制
* [FDDI](siyuan://blocks/20230129154216-0o2rvvq)：fiber distributed data interface光纤分布式数据接口
* [CSMA/CD](siyuan://blocks/20230129154053-ft7rpf8)：carrier sense multiple access with collision detection带冲突检测的载波侦听多路接入

  [CSMA/CA](siyuan://blocks/20230204152633-5re3i38)：carrier sense multiple access with collision avoidance带冲突避免的载波侦听多路接入
* [FCS](siyuan://blocks/20230129164912-9lhmp0p)：frame check sequence帧校验序列

  CRC：cyclic redundancy check循环冗余校验
* [SAP](siyuan://blocks/20230129163749-85wkhdu)：service access point服务接入点

  DSAP：destination目的服务接入点

  SSAP：source源服务接入点
* [OUI](siyuan://blocks/20230129164903-pc72kaq)：organizational unique identifier网卡或接口制造商唯一标识
* [DSSS](siyuan://blocks/20230129171044-3dgc70q)：direct sequence spread spectrum直接序列扩频
* [OFDM](siyuan://blocks/20230129171622-vrapg7j)：Orthogonal Frequency Division Multiplexing正交频分多路复用技术
* [BSS](siyuan://blocks/20230129172156-3230ony)：basic service set基础服务集

  BS：base station基站

  AP：access point接入点

  SSID：service set identifier服务集标识系统

  DS：distributed system分布式系统

  ESS：extended service set
* [ip地址分配协议](siyuan://blocks/20230106151536-x30nhig)

  RARP：reverse address resolution protocol逆向地址解析协议

  BOOTP：BOOTstrap protocol自举协议

  DHCP：dynamic host configuration protocol动态主机配置协议
* [ARP](siyuan://blocks/20230206123006-g4dqp6t)：address resolution protocol地址解析协议
* [routing protocols](siyuan://blocks/20230206132625-oss6v4s)

  IGP: Interior Gateway Protocols (RIP, IGRP,  
  EIGRP, OSPF)内部网关协议

  EGP: Exterior Gateway Protocols (EGP, BGP)外部网关协议

  BGP：border gateway protocol边界网关协议

  RIP：(Route Information Protocol) 路由信息协议

  IGRP：(Interior Gateway Route Protocol) 内部网关路由选择协议

  EIGRP：(Enhanced IGRP) 增强网关路由选择协议

  OSPF：(Open Shortest Path First) 开放最短路径优先

  DVP: Distance-Vector Protocols (RIP, IGRP)距离矢量协议

  LSP: Link State Protocols (OSPF)链路状态协议
* [VLSM](siyuan://blocks/20230206141554-1f522el)：variable-length subnet mask可变长子网掩码
* CIDR：无类别域间路由，Classless Inter-Domain Routing

  CIDR把几个标准网络合成一个大网络
* [ICMP](siyuan://blocks/20230206142506-qfzyrws)：internet control message protocol因特网控制报文协议

  PING：packet internet groper因特网包探索器
* [TCP](siyuan://blocks/20230208154815-pemmxf5)：transmission control protocol传输控制协议

  MSS：maximum segment size最大报文段长度

  TPDU：transport protocol data unit传输协议数据单元

  UDP：user datagram protocol用户数据报协议
* [ARQ](siyuan://blocks/20230208162121-8b2he5o)：automatic repeat request自动响应重传
* [NAT](siyuan://blocks/20230208175629-xgpb1wd)：network address translator网络地址转换

  PAT：port address translator端口地址转换
* [session layer applications](siyuan://blocks/20230209203657-916klxs)
* [ASCII](siyuan://blocks/20230209204046-9k25rlc): American Standard Code for Information Interchange

  EBCDIC: Extended Binary Coded Decimal Interchange Code
* [POST](siyuan://blocks/20230210154123-z57zyg2)：power on self test加电自检
* [SPF](siyuan://blocks/20230206135453-2ytgp2i)：shortest path first最短路径优先
* [IETF](siyuan://blocks/20230206141534-cntijru)：internet engineering task force互联网工程任务组
* [NBMA](siyuan://blocks/20230213232352-lpnobs4)：non-broadcast multi-access非广播多路接入
* [BPDU](siyuan://blocks/20230216154951-f9xlffe)：bridge protocol data unit桥接协议数据单元
* [ISL](siyuan://blocks/20230218135044-1pam87e)：inter-switch link
* [CSU](siyuan://blocks/20230218143043-6ddvqru)：channel service unit信道服务单元

  DSU：data service unit数据服务单元
* [SVC](siyuan://blocks/20230218143812-krbnljk)：switched virtual circuit交换虚拟环路

  PVC：permanent virtual circuit永久虚拟环路

### 网络拓扑

总线型，环形，星形……

可靠性最高的拓扑：网形拓扑

### 网络类型

* 双绞线以太网（10BASE-T）：使用UTP
* 快速以太网（100BASE-T）

  * 100BASE-TX, 100-BASE-T4, 100BASE-T2: 100Mb/s, twisted pair
  * 100BASE-FX: 速率同，使用光纤
* 1000BASE-T，utp

  * 1000BASE-LX: 多模光纤/单模光纤，长波激光信号源
  * 1000BASE-SX: 多模光纤，短波
  * 1000BASE-CX: 铜缆coaxial
  * 1000BASE-ZX: 单模光纤

## OSI七层模型

### 1-Physical

#### 1.1 LAN 介质

两种干扰：[EMI，RFI](siyuan://blocks/20230106153313-wwsvlf3)

* ==twisted pair==【短距离100m】【10-100Mbps】

  * **STP & ScTP**: shielded twisted pair & screened twisted pair

    比utp抗干扰能力强，但是重量大价格贵，屏蔽层必须接地

    stp和sctp的connector都是自己独有的
  * **UTP**: unshielded twisted pair【最便宜】

    ==RJ-45 Connector==: 减少noise

    缺点：容易受到电子噪音和干扰影响，支持的长度短

    UTP分类与规格：七类线

    * straight cable：以太网线？同类设备
    * rollover cable: console线
    * crossover cable: 连接交换机
* **coaxial** 【远距离500m】【比光缆便宜，比twisted pair贵】

  BNC Connector

  优点：可以在没有中继器的情况下传输较远距离
* **fiber-optic**【更长距离】【最贵】【快】

  Multimode Connector：接口不容易损坏

  * single mode(单模光纤): WAN【3000m】, fast, 直径小(less dispersion能量损耗)【使用[ILD](siyuan://blocks/20230106153754-3dccot2)和[LED](siyuan://blocks/20230106153803-7vy6zzh)发射】
  * multimode(多模光纤): LAN【2000m】，直径大

#### 1.2 5-4-3-2-1 rule

![image.png](计算机网络(22Fall)/image-20230106164334-fjlo74j.png)

1个大冲突域：4个中继器/集线器将网络分为5段，3段网络，2段链路

#### 1.3 数据通信

* 信号

  模拟信号：连续波

  数字信号：离散值
* 传输速率

  无噪信道：C = W log~2~ L (bps)【W：带宽Hz，L：表示数据的信号电平数量】

  噪声信道：C = W log~2~ (1+S/N)【S/N信噪比】
* 波特率/比特率：波特率表示信号每秒钟变化次数，比特率表示每秒钟传输二进制位数

【重点：数据编码方式】

* ==单极性编码==：零电平-0，正电平-1

  缺点：分辨结束和开始，需要时钟同步，连续信号累加
* 极化编码

  * ==不归零制码==(NRZ)

    * 电平编码：负电平-0，正电平-1（缺点同单极性）
    * 反相编码：电平一次翻转-1，无电平变化-0（有限同步）
  * ==归零制码==(RZ)：负电平-0，正电平-1，比特中位跳变零电平

    优点：本身带有同步信息，不易出错

    缺点：占用带宽
  * 双相位编码

    * ==曼切斯特码==：每位中间一个跳变（低到高-0，高到低-1）

      比RZ码效率高
    * ==差分曼切斯特==：每位位前跳变表示数据（有跳变-0，无跳变-1），位中跳变表示时钟
* 双极性编码

  * 双极性传号交替反转码(AMI)：零电平-0，正负电平跃迁-1

【多路复用】

* TDM：time division multiplexing时分复用
* FDM：frequency division multiplexing频分复用
* WDM：wavelength division multipexing波分复用
* CDM：code division multiplexing码分复用

  * CDMA：code division multiple access码分多址，各个用户使用不同码型

【通信方式】

* 单工：信号单向传输
* 半双工：信号可以双向传输，但是不可以同时
* 全双工：信号可以同时双向传输

### 2-Data Link

主要任务：差错通知，网络拓扑，**流控制**

frame：封装形式（协议数据单元PDU：protocol data unit）

【LLC和MAC构成网卡驱动程序】

#### 2.1 LLC

【IEEE 802.2】

transitions up to the network layer（向上到网络层的过渡）；逻辑上标示不同协议类型并封装他们

提供三种服务：

* [无连接](siyuan://blocks/20230206125054-ong93dw)无应答：以太网标准服务（可靠连接，实时任务，局域网）
* 无连接有应答：wifi【IEEE 802.11】
* [面向连接](siyuan://blocks/20230206124657-al67r0m)带应答：蓝牙

【封装】

![image.png](计算机网络(22Fall)/image-20230129163748-1nrenx1.png)

SAP：service access point服务接入点，LLC通过SAP和network layer传输数据，data link和network通信接口

DSAP：destination目的服务接入点

SSAP：source源服务接入点

#### 2.2 MAC

【IEEE 802.3】

transitions down to media（向下到介质层的过渡）；定义如何在物理线缆上传输帧；处理物理寻址；定义网络拓扑；定义线缆规章

MAC协议：用来确定共享介质环境中哪台计算机允许传输数据

* 不确定的（先来先服务）

  Ethernet：逻辑总线，物理星形或扩展星形拓扑

  ==CSMA/CD==：带冲突检测的载波侦听多路接入——先侦听线路，空闲发送数据，否则等待；发送数据同时侦听线路，检测到冲突广播拥塞信号，后退算法决定哪个设备再次接入。
* 确定的（轮流）

  token ring：逻辑环形/物理星形拓扑【IEEE 802.5】

  FDDI：逻辑环形/物理双环形拓扑

==【Frame format】==

![image.png](计算机网络(22Fall)/image-20230129161417-5xvmc6c.png)

* preamble：前7字节10101010，最后一个字节10101011
* dest&source：源mac地址和目的mac地址（48位-网卡）

  mac地址格式：前24位OUI，后24位制造商分配，通常写为12位16进制表示

  广播地址：FFFF.FFFF.FFFF

  广播发生情况：目的mac地址未知/目的地是全体主机
* length：data的字节数
* data：最少46Bytes，最多1500Bytes(MTU: maximal transfer unit)
* FCS：帧校验序列，数据链路层mac协议尾部字段，是一段4字节的循环冗余校验码（CRC）

#### 2.3 Wireless LAN

##### IEEE 802.11分类

* 802.11【Wi-Fi】

  DSSS：direct sequence spread spectrum直接序列扩频，在发射端扩展信号的频谱，而在接收端用相同的扩频码序列进行解扩【1-2Mbps】（802.11/802.11b）
* **802.11b**

  11Mbps

  also support 802.11 for 1 and 2 Mbps data rates for DSSS only

  operating within 2.4GHz
* **802.11a**

  54bps【standard 20-26bps】

  operating in 5GHz
* **802.11g**

  OFDM：orthogonal frequency division multiplexing正交频分多路复用技术（802.11g）
* **802.11n**

  next generation WLAN

  108bps【theoretically 500-600Mbps】
* 802.1q

  见[VLAN](siyuan://blocks/20230216172324-pji302l)

##### 模式

* infrastructure mode：基础建设模式

  ==Base Service Set(BSS)==: Base Station(BS)【Access Point(AP)】+hosts

  AP：Service Set Identifier(SSID)+a channel

  Extended Service Set: 多个BSS通过DS(distributed system)连接
* ad-hoc mode：蓝牙

##### 连接过程

* active scanning: 探针请求(probe request)【包括SSID】，AP回应
* passive scanning: 监听beacon management frames

##### Frames

* control frames
* management frames
* data frames

  ![image.png](计算机网络(22Fall)/image-20230204152425-1wiy462.png)

  ![image.png](计算机网络(22Fall)/image-20230204152448-du3ka7c.png)

##### ==CSMA/CA==

wireless使用CSMA/CA：站只能知道nearby station的传输情况，无法检测，只能避免

* hidden station problem

  两个站点同时给另一个站点发送
* exposed station problem

  周围站点传输影响空闲站点传输

原理：发送数据前以控制短帧刺激接收站发送应答短帧，周围站点监听到避免发送

过程：

1. A向B发送RTS（Request To Send）帧，A周围的站点在一定时间内不发送数据，以保证CTS帧返回给A；
2. B向A回答CTS（Clear To Send）帧，B周围的站点在一定时间内不发送数据，以保证A发送完数据；
3. A开始发送
4. 若控制帧RTS或CTS发生冲突，采用二进制指数后退算法等待随机时间，再重新开始。

### **3-network**

PDU：packet

#### 3.1 ==IP packet==

ip协议是routed protocol，network layer 协议，IPX协议簇（某网络操作系统协议）相当于ip协议

![image.png](计算机网络(22Fall)/image-20230204160237-om3qtvq.png)

* 版本：IPv4-0100，IPv6-0110
* 首部长度：单位-4字节，min-5，max-15
* 总长度：首部和数据之和，max-65535bytes(2^16^)
* 标识(identification)：数据报标识，用于数据报分片-计数器
* 标志：0/MF/DF，3位，MF=0表示最后一个分片
* 片偏移：单位-8字节，某片在原分组中的相对位置
* 生存时间TTL(Time to Live)：数据报在网络中可通过的路由器数的最大值。min-1, max-255(2^8^-1)
* 协议：数据报携带数据使用协议

  一般是传输层协议，比如**6 TCP，17 UDP**；但也可能是网络层协议，比如**1 ICMP**；也可能是应用层协议，比如**89 OSPF**
* 首部检验和：只检验首部

  ![image.png](计算机网络(22Fall)/image-20230204162503-d6t8rh4.png)
* 源地址&目的地址：4字节ip地址

#### 3.2 IP address

Network ID & Host ID【network id is assigned by ARIN】

【分类】

![image.png](计算机网络(22Fall)/image-20230204163145-7tnhq46.png)

可分配主机数目：2^n^-2(全0-网段地址，全1-广播）

==私有地址==：

![image.png](计算机网络(22Fall)/image-20230204163742-r6asq4d.png)

解决ip地址耗尽的方法：NAT，CIDR，IPv6(加16位地址）

**【组播ip地址】D类地址**

#### 3.3 ==subnet==

子网由网络管理员在本地分配

![image.png](计算机网络(22Fall)/image-20230205220523-tymh1ii.png)

subnet借位数：min-2，max-(host位数-2)【至少剩下两位给主机，只保留1位取0与网段冲突，取1与广播地址冲突】

划分子网造成地址浪费

![image.png](计算机网络(22Fall)/image-20230205225721-ush07xk.png)

##### 子网掩码

用于计算子网地址，子网掩码与ip地址做按位与运算得出子网地址

* class A: 255.0.0.0
* class B: 255.255.0.0
* class C: 255.255.255.0

##### ==子网划分==

1. 确定哪类网（A/B/C）
2. 多少个子网，多少个主机-确定借位数
3. 计算子网掩码
4. 确定主机可用地址范围

可用子网 = 可能子网 - 2

可用主机 = 可能主机 - 2

#### 3.4 第三层设备-Router

【path determination】

【interface/port】每个接口必须有一个独立的网段地址

[【ip地址分配】](siyuan://blocks/20230106151536-x30nhig)

* 静态分配(static sddressing)：手动分配
* 动态分配(dynamic addressing)

  RARP：reverse address resolution priotocol

  BOOTP: BOOTstrap Protocol

  DHCP: dynamic host configuration protocol

#### 3.5 ARP protocol

将MAC地址对应到ip地址

**原理：**

每个主机维护一个本地ARP表（MAC地址和IP地址一一对应）【存在RAM中】

如果不存在目的ip地址，发送广播，目的主机发现ip地址与自身匹配，发送响应-源主机加入ARP表

**与不在一个网段通信：**

* default gateway(默认网关): 网段路由接口ip
* proxy ARP(代理ARP): 中间设备（如路由器）代表目的端发送ARP应答

#### 3.6 network services

* **面向连接**的网络服务（connection oriented network service)：在传输数据前发送者和接收者之间建立连接

  * 环交换（circuit switched)：必须有一条通路（All packets travel sequentially across the same channel, or more commonly, across the same virtual circuit.）
* **无连接**（connectionless)：分别对待每一个包（不同路径，不同顺序）【**ip是一个无连接系统**】

  * 包交换(packet switched)

#### 3.7 可路由协议和路由协议

routed protocols：direct user traffic

routing protocols：maintain tables

##### 可路由VS不可路由

* routed/routable protocol：提供对第三层网络层的支持，可以被路由器转发
* non-routable protocol：不支持网络层，不可以被路由器转发（如NetBEUI）

##### 路由协议(routing protocol)

用于路由器之间的协议，动态获取路由信息，添加到路由表中

具体内容见[路由器相应协议](siyuan://blocks/20230206122851-4p2pz3g)部分

#### 3.8 ==VLSM==

classful routing有类路由：一个网络只能使用一个子网掩码

VLSM支持使用0号子网

**分配示例**：先分配给需要最多host数目的子网，依次往下分配给host第二多的子网，每一次分配都是在上一次没有分配的子网下开始进行的

![image.png](计算机网络(22Fall)/image-20230207215848-ljmub3v.png)

Perth需要6位给host, 192.168.10.0/26 (255.255.255.192)【**00**00 0000】

KL需要5位host, 192.168.10.64/27 (255.255.255.224)【**010**0 0000】

Sydney需要4位host, 192.168.10. 96/28 (255.255.255.240)【**0110** 0000】

Singapore也4位, 192.168.10.112/28 (255.255.255.240)【**0111** 0000】

**WAN link需要2个ip地址**, 192.168.10.128/30, 分配完新加坡就从128开始

【支持VLSM的protocol】

* OSPF
* Integrated Intermediate System to Intermediate System (Integrated IS-IS)
* EIGRP
* RIP v2
* static routing

【路由聚合】借位数减少，路由表中条目减少

![image.png](计算机网络(22Fall)/image-20230207230221-rui92m9.png)

#### 3.9 ICMP

允许主机或者路由器报告差错情况，提供异常情况报告

只是ip层协议，数据报首部加上ICMP报文组成ip数据报发送

【报文格式】

![image.png](计算机网络(22Fall)/image-20230207230835-gfx1zmb.png)

【类型】

* 差错报告报文

  ![image.png](计算机网络(22Fall)/image-20230207231325-dmmcpo2.png)

  【不发送ICMP特例】

  * ICMP 差错报告报文
  * 第一个分片的数据报片的所有后续数据报片
  * 具有多播地址的数据报
  * 具有特殊地址（如127.0.0.0或0.0.0.0）<br />
* 查询报文

==【PING】==

利用ICMP回送请求和回送回答报文实现，用来测试主机之间连通性

**应用层直接使用网络层**，不需要通过传输层

### **4-transport**

PDU：segment

【functions】

* 将上层应用的数据分段
* 建立端到端的操作
* 将段从一台主机发送到另一台
* **flow control** and **reliability**

#### 4.1 port

标准RFC1700

0~255：public端口给固定应用

0~1023：well-known端口

【著名端口】

TCP 21端口：FTP 文件传输服务

TCP 22端口：SSH secure shell安全外壳协议，对密码进行加密传输验证

TCP 23端口：TELNET 终端仿真服务

TCP 25端口：SMTP 简单邮件传输服务

**UDP 53端口**：DNS 域名解析服务

67：Bootstrap protocol server

UDP 68：DHCP

UDP 69：TFTP

**TCP 80端口**：HTTP 超文本传输服务

89：ospf

TCP 109/110端口：POP3 “邮局协议版本3”使用的端口

UDP 161/162：SNMP

**TCP 443端口**：HTTPS 加密的超文本传输服务

UDP 520：RIP

#### 4.2 ==TCP==

##### properties

* reliable可靠的
* connection oriented面向连接的
* 重传所有丢失的或错误的报文【stop-and-wait protocol】
* 使用确认acknowledgments
* 提供**流控制**

##### 报头格式

![image.png](计算机网络(22Fall)/image-20230208162446-24xj70e.png)

* 端口号各占2字节
* 序号：每个字节一个序号，值代表第一个字节序号
* 确认号：希望收到对方下一个报文段数据的第一个字节序号
* 数据偏移：TCP 报文段的数据起始处距TCP 报文段的起始处的长度
* 保留字段：以后使用，目前置0
* 6位标志位

  * URG：1-紧急指针字段有效
  * ACK：1-确认号有效
  * PSH：1-尽快交付，不等待缓存填满
  * RST：1-释放连接重新建立连接
  * SYN：1-连接请求或连接接受报文
  * FIN：1-数据发送完毕，释放连接
* 窗口：让对方设置发送窗口依据，单位字节
* 检验和：检验包括首部和数据
* 紧急指针：指出本报文段中紧急数据有多少字节
* 选项与填充：

  MSS(maximum segment size)：告诉对方缓存能够接受的报文数据字段最大长度，单位字节

  填充：使整个首部长度是4字节整数倍

##### flow control

* ==sliding window滑动窗口==

  **ARQ**：automatic repeat request自动响应重传

  ![image.png](计算机网络(22Fall)/image-20230208171624-j82zrjt.png)
* congestion avoidance

##### connection management

* **3次握手建立连接**

  ![image.png](计算机网络(22Fall)/image-20230220103840-ksc7j5d.png)

  1. server监听，client发送TCP segment [SYN=1,ACK=0]
  2. Server checks if exists service process monitoring the port

      * 不存在，发送TCP segment [RST=1]
      * 存在，决定接受[SYN=1,ACK=1]还是拒绝连接
  3. client发送TCP segment [SYN=0,ACK=1]
* 4次握手释放连接

  ![image.png](计算机网络(22Fall)/image-20230220103817-vylk2yy.png)

  1. client发送给server，[FIN=1,seq=u]
  2. server发送给client [ACK=1,seq=v]
  3. server发送给client [FIN=1,ACK=1]
  4. client发送给server [ACK=1]

      在彻底关闭连接之前，client必须等待2MSL时间：确保ACK可以发送到server

##### stop-and-wait protocol

* Each segment and ACK must have ID
* The resend-time must be more than average-travel-time *2
* 效率低

![image.png](计算机网络(22Fall)/image-20230208170213-815uq1v.png)

#### 4.3 UDP

报头小，no delay, no congestion control

适用于对速率敏感的场合

##### properties

* unreliable不可靠
* 无连接，无确认，无流控制

##### 使用udp的协议

* RIP
* DNS
* SNMP
* TFTP
* DHCP

##### 报头格式

![image.png](计算机网络(22Fall)/image-20230208175115-vs3vwpf.png)

udp最小8字节（仅包含首部）

检验和包括首部和数据

【ip数据报检验和只检查首部，tcp和udp都检查首部和数据】

#### 4.4 Socket

1. 表达形式：ip地址+端口号
2. 套接字对（source, destination）【point-to-point full-duplex点对点全双工】
3. **TCP不支持组播和广播**

#### 4.5 NAT&PAT

RFC 1631

* 静态NAT：ip地址内网和外网一对一映射，保持不变
* 动态NAT：ip转换随机，先来先服务

PAT：对外出数据包的源端口进行转化，使内部网络所有主机可以共享**一个**合法外部ip地址

### 5 session&presentation&application

#### 5.1 session

interhost communication

【Dialog Control】

* Two-Way Alternate (TWA)
* Two-Way Simultaneous (TWS)

【checkpoint】校验点

恢复通信，dialogue seperation

==【Applications】==

* Network File System (NFS)
* Structured Query Language (SQL)
* Remote-Procedure Call (RPC)
* AppleTalk Session Protocol (ASP)
* DNA Session Control Protocol (SCP)

#### 5.2 presentation

将数据以接收设备可以理解的方式呈现

* data formatting

  * ASCII: American Standard Code for Information Interchange

    MIME：multipurpose internet mail extensions多用途互联网邮件扩展类型
  * EBCDIC: Extended Binary Coded Decimal Interchange Code广义二进制编码的十进制交换码
  * GIF: Graphic Interchange Format图形交换格式
  * JPEG: Joint Photographic Experts Group联合图像专家组
* data compression
* data encryption

#### 5.3 application

一些应用详见[协议集合](siyuan://blocks/20221124205431-8do7ken)

## TCP/IP四层模型

OSI 1-2  <---> network access

OSI 3     <---> Internet

OSI 4     <---> transport

OSI 5-7  <---> application

> OSI模型和tcp/ip模型的异同点
>

相同：

* 两种模型都体现了分层设计的思想，都是下层服务上层
* 两种模型都有网络层、传输层和应用层

不同：

* 层数不同
* TCP/IP支持跨层封装，但是OSI不支持，只允许相邻层之间的交互。
* TCP/IP**只支持IP网络协议**，而 OSI支持多种网络层协议
* OSI是理论上的标准，**TCP/IP是事实上的标准**

## 各层协议集合

### Data link layer

MAC

### ==N====etwork layer==

#### ARP

data link & network layer，[address resolution protocol](siyuan://blocks/20230206123006-g4dqp6t)

#### IP(Internet Protocol)

[网络层协议](siyuan://blocks/20230204160036-5fusoz4)

#### ICMP

[internet control message protocol](siyuan://blocks/20230206142506-qfzyrws)

#### 路由协议

见下方路由器及相应协议

### Transport layer

#### TCP&UDP

transport layer

TCP(Transmission Control Protocol)

UDP(User Datagram Protocol)

### Application layer

* Telnet：连接远程主机
* FTP: file transfer protocol（使用tcp）
* TFTP: Trivial file transfer protocol（使用udp）
* SMTP: simple mail transfer protocol(tcp)
* SNMP: Simple Network Management Protocol简单网络管理协议
* HTTP: hypertext transfer protocol

  HTML: hypertext markup language

  URL: universal resource locator

  css: cascading style sheet
* POP：post office protocol（tcp）
* DNS：domain name system 域名系统

  TLD: top level domain顶级域名

## **路由器及相应协议**

### 路由器内部结构

![image.png](计算机网络(22Fall)/image-20230210153347-rpjcg6r.png)

* RAM：存储临时数据，如路由表，ARP cache，报文缓存【断电失去所有数据】
* NVRAM：存储备份文件和启动文件
* Flash：EEPROM，保存Cisco IOS(Internet Operating System)
* ROM：只读内存，加载引导程序和操作系统备份【POST：power on self test加电自检】

### 路由器启动过程

1. POST：执行加电自检，对所有硬件模块执行ROM中的诊断
2. 检验CPU，内存，接口的基本操作
3. 初始化软件

    1. 在cpu上执行引导程序
    2. 查找操作系统
    3. 加载操作系统
    4. 加载配置文件并执行

        没找到配置文件进入setup模式

### 路由器数据传输

两个function合作：

path determination：路径选择，选择最合适接口转发数据包

switching：转发，在一个接口接收数据包，另一个接口转发

【administrative distance】

管理距离，提供路由可靠性参数，范围0~255

管理值越小越可靠，1是默认值

### ip地址分配协议

#### RARP

#### BOOTP

#### DHCP

使用**udp广播**实现高效分配ip地址

![image.png](计算机网络(22Fall)/image-20230209234050-iscy12p.png)

【DHCP欺骗】

非授权DHCP服务器应答客户请求

启用DHCP snooping防范

### routing protocols

#### 静态路由

管理员手动获取路由器中的路由信息

#### 动态路由

利用路由协议更新路由信息，维护路由表，定期告诉邻居

【分类一】

* 内部网关协议IGP：用于自治系统

  * RIP
  * OSPF
  * IGRP
  * EIGRP
* 外部网关协议EGP：用于自治系统之间

  * EGP
  * BGP（使用tcp）

==【分类二】==

![image.png](计算机网络(22Fall)/image-20230210181841-cagkjjd.png)

* **DVP（distance-vector protocols)**

  通过计算距离矢量选择最佳路径，频繁周期性更新路由表，每次将**整张路由表**发给周围路由器

  DVP不允许路由器知道整个网络的确切拓扑

  使用算法：**Bellman-Ford alogorithm**

  【问题】路由环路(routing loops) -> counting to infinity(无穷计数)

  解决方法：

  1. **定义最大跳数**：16作为无穷大，超过最大跳数丢弃报文
  2. 路由毒化(route poisoning)：路由信息失效时将该条路由表设为16（无穷大）再发布出去
  3. 水平分割(split horizon)：由一个接口发出去的信息不可以再朝这个接口发送
  4. 抑制定时器(hold-down timers)：一条路由信息无效之后一段时间内该条路由处于抑制状态，不接收关于同一目的地址的路由更新

  【DVP protocols】

  * RIP
  * IGRP
* **LSP（link state protocols)**

  每个路由器都了解整个网络的拓扑结构，利用算法决定最短路径，每次更新只传递更新

  算法：**SPF(shortest path first)最短路径优先**

  * link-state advertisements(LSAs) 链路状态通告
  * link-state database(LSDB) 链路状态数据库

  【执行过程】

  1. routers之间交换LSA
  2. 建立拓扑数据库topological database
  3. SPF算法计算网络可到达与否(network reachability)
  4. router在路由表中列出最佳路径和到目标网络的port端口

  【问题】

  * 处理器和内存需求：LSP比DVP对处理器和内存的需求更高
  * 带宽需求：初始化时packet flooding会使可使用带宽临时减小

  【DVP protocols】

  * OSPF
* **混合协议（hybrid protocols）**

  * OSI's IS-IS：intermediate System-to-Intermediate System
  * Cisco's EIGRP：Enhanced interior gateway protocol

##### **RIP**

**使用udp**

routing information protocol，适用于小型网络

【属性】

* Interior Gateway Protocol(IGP)
* Distance-Vector Protocol(DVP)

【内容】

number of hops路由器跳转次数（max-15, infinity-16）

每30s更新一次(向邻居更新整张路由表），不会总是选择最快路径

【版本】

v2->v1

v1和v2配置都很简易

v1的限制：

* 不支持VLSM和CIDR（不发送子网掩码）
* 255.255.255.255作为广播地址
* 不支持认证

v2特性：

* 使用holddown timer和split horizon防止路由环路，默认180s
* 认为16跳无限长
* 支持VLSM（发送子网掩码）
* 以224.0.0.9作为广播地址
* 支持authentication

##### IGRP&EIGRP

了解名字

##### **OSPF**

**直接使用ip**

标准：IETF-internet engineering task force/RFC 2328

使用neighborship database&topology database，算法：dijkstra shortest path first(SPF)

优点：适用于大型网络，robust健壮，scalable可扩展

【术语】

* link：网络设备之间的物理连接

  link-state：link状态，包括接口信息和邻接路由器关系
* cost：基于**带宽**的连接上的值（带宽越小，cost越高）
* **area**：一组网络或路由器拥有相同area ID就被划分为一个area

  32位标识，可以采用ip格式(0.0.0.0)或十进制

  单区域area 0，多区域必须都要连接到area 0(中枢链路)
* designated router(**DR**)：指定路由器，在一个网络中选举出来代表所有路由器的路由

  backup designated router(BDR)：备份DR

  每个路由器和DR&BDR建立邻接关系

  DR使用**224.0.0.5**向其他路由器发送链路状态信息(link-state information)

  链路拓扑改变时其他路由器通过**224.0.0.6**发送给DR/BDR

![image.png](计算机网络(22Fall)/image-20230214095022-f7lajds.png)

【OSPF路由协议包】

* Hello

  周期性（点对点网络默认每10s发送一次报文，NBMA30s一次）

  发送地址为224.0.0.5

  hello报文type = 1

  ![image.png](计算机网络(22Fall)/image-20230214095122-xy81z96.png)
* DBD: database description
* LSR: link-state request
* LSU: link-state update
* LSAck: link-state acknowledgement

【OSPF操作】

1. 建立邻接关系

    周期性发送hello报文，找到邻居：加入邻接数据库
2. 选举DR和BDR（如果需要）

    priority + router ID 最大的是DR，第二大是BDR

    priority: 1-255 默认1，优先级越高越大，0表示永远不会成为DR

    router ID: loopback ip address环回地址（即类似ip地址），没有环回地址选择最大接口地址（如果接口关闭需要重新建立邻接关系同时重新发送LSA）

    【如果新的优先级更高的路由器加入网络，当前DR和BDR**不变**，如果当前DRfail新的高优先级路由器可以成为BDR，原来BDR成为DR】
3. 发现路由

    DR/BDR发送LSA，其他路由器发送DBD/LSR
4. 选择合适的路由

    使用**SPF算法建立树**，以cost作为衡量标准，16位（1-65535）

    ![image.png](计算机网络(22Fall)/image-20230214103836-9g0qj78.png)
5. 维护路由信息

    周期性交换hello报文发现新的邻居，4倍interval没收到认为路由死掉

【网络类型】

* broadcast multi-access, 广播多路接入（如以太网）

  ✔️需要DR election
* point-to-point点对点网络

  ❌不需要DR election
* non-broadcast multi-access(NBMA)非广播多路接入

  ✔️需要DR election

## 局域网交换与VLAN

### switching

【基本功能】建立维护交换表；从接口交换帧到目的端

#### 对称交换&非对称交换

对称交换：提供**带宽相同**端口交换（瓶颈：user尝试访问其他网段服务器）【10或100Mbps】

非对称交换：减少瓶颈发生的可能性-将服务器和高带宽端口连接【100Mbps】（非对称交换需要交换机中有**内存缓冲**）

#### 内存缓冲

memory buffering，存储目的地和传输数据

* port-based：每个端口以队列形式存储packet，可能因为端口忙碌延迟传送
* shared memory：所有端口共享

#### 交换方法

* **store-and-forward**(存储转发)：交换机接收整个帧，计算尾部CRC，再发送到目的地
* **cut-through**(直通转发)：

  * fast-forward：快速直通转发，只检查目的MAC地址，然后直接转发
  * fragment-free：无碎片直通转发，只读取data前64字节（减少错误）

#### 各层交换

【第2层交换】基于硬件高速交换，低延迟低代价

【第3层交换】基于硬件的packet转发

【第4层交换】基于第三层

### Spanning-Tree Protocol

减少冗余路径不增加延时：通过计算稳定的生成树拓扑

#### 决定顺序

lowest root BID(bridge identification） 

lowest path cost to root bridge  

lowest sender BID 

lowest port ID

==【BID】== a bridge id - 8 bytes网桥id

2字节优先级+6字节MAC地址，默认优先级32768

【path cost】

![image.png](计算机网络(22Fall)/image-20230216171053-3llem71.png)

#### BPDU

Spanning-tree frames( bridge protocol data units-BPDU)：用来决定生成树拓扑

1. STP建立一个根节点叫做root bridge

    根据**最低的BID**选举根节点，如果所有交换机优先级相同，选择最小MAC地址
2. 从根节点开始建立生成树，冗余链路被阻塞，冗余链路上的packet也被丢弃
3. 交换机发送BPDU来形成拓扑结构

#### 5种状态

* blocking：不转发帧，监听BPDU
* listening：不转发帧，监听数据帧
* learning：不转发帧，学习地址
* forwarding：转发帧，学习地址
* disabled：不转发帧，不监听BPDU

#### STP收敛步骤

1. 选举root switch：根桥所有端口都是指定端口，指定端口都处于forwarding状态
2. 选举root ports：在剩下的每一个switch中选择1个根端口（从非根桥到根桥花费最低）
3. 选择指定端口：每个网段有一个指定端口，指定端口是在到根桥花费最低的网桥上选取的，这台交换机上的其他**非指定端口会被阻塞**

### VLAN

逻辑网络设备或用户分组；单一广播域；在第2/3层工作

用户基于port/MAC/ptotocol/application分组

不同vlan之间通过**路由器**通信

#### trunk link&access link

交换机与交换机之间的骨干链路，用于同一vlan通信，减少端口浪费【high speed links: >= 100Mbps】

> 如何解决共用trunk导致的数据包混淆问题？
>

* frame filtering(帧过滤)：检查帧当中的MAC地址或者第三层使用协议

  【交换表/address table】记录主机MAC地址和对应vlan（存储在交换机中）
* frame tagging(帧标记)：在每个帧头部放置标记位，进入backbone之前加上，离开backbone之后去除

  【IEEE 802.1q】添加标记位的协议

  **ISL**: inter-switch link，在头部加上26字节，在尾部添加4字节CRC

**access link**: 只属于一个vlan的link，任何vlan中的主机不知道vlan存在（完全透明）

==trunk link==: 支持多个vlan（可以支持所有，也可以配置有限的vlan），连接交换机之间或交换机和路由器

【vlan trunking protocol-VTP】

#### implementation

##### static

静态vlan由管理员手动分配

优点：安全，容易配置监控

##### dynamic

switch维护一张交换表动态查找相应的主机地址

##### port-centric

路由器分配一个interface给某一个vlan，方便管理，有更高的安全性

也可以多个vlan共享一个路由器interface

## 广域网-WAN

WAN在OSI的前三层工作，主要是物理层和数据链路层

### 设备

modem调制解调器，主要有CSU&DSU

CSU：channel service unit信道服务单元

DSU：data service unit数据服务单元

CPE：customer premises equipment客户端设备

CO：central office中心局(CO switch：离WSP提供服务最近的设备接入点)

Toll Network：collection of switches/trunks in WAN cloud

ISDN terminal adapter

### Circuits

#### Switched Virtual Circuits(SVC)

WAN paths to the destination，有established和terminated两种状态

【三个阶段】

* circuit establishment
* data transfer
* circuit termination

【**telephone service电话服务和ATM使用SVC**】

（ATM: async transfer mode异步传输方式)

带宽增加，cost减小

#### Permanent Virtual Circuits(PVC)

只有一种模式data transfer

【X.25和frame relay使用PVC】

### WAN and OSI

从广域网服务提供商或PTT(post telephone and telegraph)处获取接入广域网服务

#### physical layer

物理层定义了DTE和DCE之间的接口

DCE-service provider, DTE-client

#### data link layer

描述数据如何在不同系统之间的单一链路上传输，包括各种协议等

### Accessing methods

#### ==PPP==

Point-to-Point Protocol，第二层协议

IETF开发，用来替代SLIP（只支持ip，不支持动态分配ip地址）

包含一段用来识别网络层协议的字段

在建立连接的过程中可以检查链路质量

提供**PAP**（Password Authentication Protocol）和**CHAP**（challenge handshake authentication protocol）认证

##### components

* 使用HDLC作为第三层报文的封装
* 使用LCP（Link Control Protocol）：建立链路，配置链接选项，测试链路质量
* 使用NCP（network control protocol）：选择和配置第三层协议

##### 会话建立和终止

1. 链路建立和配置协商（LCP）

    每个PPP设备发送LCP来开启连接，设备可以协商LCP中携带的压缩或认证协议
2. 链路质量测试

    发送和接收LCP来测量error rate

    认证在网络层协议配置开始之前发生

    LCP可以延迟网络层协议信息的传输直到测试阶段完成
3. 网络层协议配置（NCP）
4. 链路终止

    **LCP可以在任何时间终止链路**：用户请求；链路质量不好；超时

    LCP终止链路会通知网络层协议

##### PAP

密码验证协议，双向握手

用户名和密码对不停的在链路上发送（明文形式）直到验证通过或连接终止，建立连接前只认证一次

##### CHAP

询问握手验证协议，三次握手

host发送challenge message给remote node, remote node返回一个加密值，包括收到的challenge和用户名密码

host检查匹配承认认证

#### HDLC

high-level data link control

ISO standard，不同供应商之间的HDLC不兼容，cisco's default encapsulation for serial lines，只有两台路由都使用Cisco的IOS时才使用HDLC（否则同步PPP）

HDLC支持point-to-point和multipoint配置

没有窗口或流控制

【LAPB】

link access procedure, balanced平衡型链路接入规程

为point-to-point提供可靠性和流控制

【frame relay】

帧中继，简单封装，没有纠错机制

#### ISDN

综合业务数字网（Integrated Services Digital Network）

从已有的电话线传输声音和数据

PPP和HDLC是两种常见的ISDN上的数据封装，默认HDLC，但是PPP更健壮

##### 两种信道

D信道：比modem速度更快的设置

B信道：更快的数据传输速率(64kps)

##### 两种访问方式

**BRI**(basic rate interface)

基本速率接口

2个带宽64kpsB信道+1个带宽16kpsD信道 = 144kps

**PRI**(primary rate interface)

主速率接口

多个B信道+1个D信道

#### ADSL

asymmetric digital subscriber line不对称数字用户线

上行和下行带宽不对称

有极限传输距离限制，与用户线直径、传输速率有关，线径越大传输速率越小，传输距离越大

##### DSL

把电话用户线原来没有使用的高端频谱给上网使用

xDSL：digital subscriber line数字用户线（x代表不同宽带方案）

* HDSL: high speed DSL
* SDSL: single-line DSL
* VDSL: very high speed DSL
* IDSL: ISDN用户线
* RADSL: rate-adaptive DSL

##### DMT

discrete multi-tone离散多音调(多载波/子信道)调制技术，采用频分复用

##### 一些设备

DSLAM: DSL access multiplexer数字用户线接入复用器

ATU：access terminal unit接入端接单元

PS：POTS splitter电话分离器

##### 第二代ADSL

提高调制效率得到更高数据率

使用无缝速率自适应技术SRA(seamless rate adaptation)

#### SONET同步光纤网

Synchronous Optical Network

sonet各级时钟都来自一个非常精确的主时钟

第 1 级同步传送信号 **STS-1** (Synchronous Transport Signal)的传输速率是 51.84 Mb/s

光信号则称为第 1 级**光载波 OC-1**，OC 表示Optical Carrier

**【SDH】**

synchronous digital hierarchy同步数字系列

ITU(international telecommunication union国际电信联盟)以sonet为基础制定出SDH

基本速率155.52Mb/s：第1级同步传递模块STM-1（synchronous transfer module）【相当于OC-3速率】

【四个光接口层】

* 光子层
* 段层
* 线路层
* 路径层

#### HFC

hybrid fiber coax光纤同轴混合网

在CATV基础上开发的居民宽带接入网

主干线路采用光纤-模拟光纤技术：头部连接到光分配结点ODN(optical distribution node)，光纤结点以下就是同轴电缆

**【UIB】**

user interface box用户接口盒

* 使用**同轴电缆**连接到机顶盒(set-top box)
* 使用**双绞线**连接到电话机
* 使用**电缆调制解调器**（cable modem）连接到计算机

  电缆调制解调器传输速率高3~10Mb/s

【FTTx】

fiiber to the...光纤到...

FTTH fiber to the home

FTTB fiber to the building

FTTC fiber to the curb路边

## 网络安全

### 四种威胁

* 截获
* 中断
* 篡改
* 伪造

【被动攻击】截获信息的攻击

【主动攻击】更改信息或拒绝用户使用资源

### 恶意程序

* 病毒：会传染其他程序的程序
* 蠕虫：通过网络的通信功能将自身从一个结点发送到另一个结点并启动运行的程序
* 特洛伊木马：程序可执行的功能超出声称功能
* 逻辑炸弹：当运行环境满足某种特定条件时执行其他特殊功能的程序

### 密钥

对称密钥：加密和解密使用相同密码体制DES

公钥密码体制：使用不同的加密密钥和解密密钥RSA

### 数字签名

* 报文鉴别：接收者能够核实发送者对报文的签名
* 报文完整性：发送者不能抵赖
* 不可否认：不能伪造

### 防火墙

防火墙内部：可信任网络，外部：不可信任网络

功能：阻止和允许

* 网络级防火墙：防止整个网络出现外来非法的入侵

  分组过滤和授权服务器
* 应用级防火墙：从应用程序来进行接入控制

  网关或代理服务器

==【ACL】==

access control list访问控制列表

根据源地址、目的地址、上层协议来确定哪些包可以通过，哪些不可以

**wildcard mask**：通配符掩码，告诉路由器哪些匹配哪些忽略，0-匹配，1-忽略

**标准ACL**：没有目的参数，需要将ACL表放置在离**保护目的地**近的路由上 **1-99**

**扩展ACL**：可以根据多种属性过滤分组，放在离**被拒绝的信源近**的地方 **100-199**
