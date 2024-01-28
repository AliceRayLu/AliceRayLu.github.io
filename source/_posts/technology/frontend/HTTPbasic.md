---
title: 【前端八股】计算机网络
date: 2024-01-14
category: [Technology,Frontend]
toc_number: false
---

# 1 网络工作原理

## 1.1 网络模型
网络模型共有两种，OSI七层模型和TCP/IP四层模型

<table>
    <tr>
        <th>OSI七层模型</th>
        <th>TCP/IP四层模型</th>
    </tr>
    <tr>
        <td> application (应用层) </td>
        <td rowspan=3> application (应用层) </td>
    </tr>
    <tr>
        <td> presentation (展示层) </td>
    </tr>
    <tr>
        <td> session (会话层) </td>
    </tr>
    <tr>
        <td> transport (传输层) </td>
        <td>  transport (传输层) </td>
    </tr>
    <tr>
        <td> network (网络层) </td>
        <td> network (网络层) </td>
    </tr>
    <tr>
        <td> data link (数据链路层) </td>
        <td rowspan=2> link (链路层) </td>
    </tr>
    <tr>
        <td> physical (物理层) </td>
    </tr>
</table>



## 1.2 传输层
- 传输层提供**端到端**的通信，即进程和进程之间的通信。（端口标识进程）
- 传输层需要对报文进行差错检测
- 提供TCP和UDP两种不同的传输协议 

【端口】
端口号长度为16bit，范围0-65535，熟知端口号0-1023

FTP-21，TELNET-23，SMTP-25，DNS-53，HTTP-80，HTTPS-443

【套接字】IP:Port
ip地址和端口号唯一确定网络中的通信进程

### 1.2.1 UDP
user data protocol-无连接的非可靠传输协议，仅提供多路复用和对数据的错误检查两种服务。

主要用于对实时性有高要求的应用，包括**DNS**、TFTP、SNMP、RTP(实时传输协议)

UDP首部为固定的8B，包括源端口号、目的端口号、长度、校验和（校验和的计算请查看计网部分内容复习）

![UDP数据报格式](https://github.com/AliceRayLu/AliceRayLu.github.io/blob/main/source/_posts/technology/frontend/assets/udp.png?raw=true)

请注意，真实情况下UDP首部还会包括一个12B伪首部，所以udp数据报的真实结构：伪首部+首部+数据，这个伪首部实际上是ip数据报的首部

### 1.2.2 TCP
transmission control protocol-面向连接的可靠服务，不提供广播或者组播服务，包括确认、流量控制、拥塞管理等。

常见应用：FTP、**HTTP**、TELNET

TCP首部包含固定20B和可变部分

![TCP数据报格式](https://github.com/AliceRayLu/AliceRayLu.github.io/blob/main/source/_posts/technology/frontend/assets/tcp.png?raw=true)

#### 1.2.2.1 建立连接-三次握手
![三次握手](https://github.com/AliceRayLu/AliceRayLu.github.io/blob/main/source/_posts/technology/frontend/assets/3shake.png?raw=true)

1. 客户端发送带SYN标志的数据包，发送一个随机序列号
2. 接收端/服务端收到后返回带有SYN和ACK标志的数据包，确认收到的序列号(ack=x+1)并发送自己的SYN包(seq=y)
3. 客户端向服务端发送确认包，两者都进入established状态开始传输数据


#### 1.2.2.2 释放连接-四次挥手
![四次挥手](https://github.com/AliceRayLu/AliceRayLu.github.io/blob/main/source/_posts/technology/frontend/assets/4shake.png?raw=true)

1. 客户端发送带FIN标志的数据包以及当前传输数据序列号
2. 服务端向客户端发送ACK确认数据包，并将剩余数据继续传输
3. 服务端将所有数据传输完毕后，向客户端发送FIN和ACK数据包
4. 客户端收到报文后发送确认数据报，服务端接收后进入closed状态，客户端在等待2*MSL（最长报文段寿命）后进入closed状态

客户端和服务端的任何一方都可以主动发起释放连接的请求

#### 1.2.2.3 重传
超时和冗余ACK会触发TCP重传
- **超时**：对每个发送报文段设置一个计时器，重传时间到期但是未收到确认就要自动重传。
- **冗余ACK**：发送方收到了两次某个报文段的ACK，通常在比当前期望的序号大的报文到达时，再次发送前面已经接收到的报文序列ACK

#### 1.2.2.4 流量控制
基于滑动窗口协议控制流量，确认报文携带允许传输的窗口大小，进行端到端的调整

#### 1.2.2.5 拥塞控制
拥塞控制一共有4种算法：
- **慢开始**：将发送方的拥塞窗口先置为1（一个最大报文段长度），收到确认后逐步增大拥塞窗口（加倍：1->2, 2->4）
    在慢开始达到了规定阈值后，改用拥塞避免算法
- **拥塞避免**：每经过一个往返时延RTT将拥塞窗口加1，出现拥塞时（未按时收到确认），将拥塞窗口重新设为1，重新执行慢开始算法（慢开始阈值改为一半？）
- **快重传**：通过发送冗余ACK包的方式来触发重传
- **快恢复**：把慢开始的阈值设为当前窗口大小的一半，然后使用拥塞避免算法将窗口缓慢增大（逐步加1）。【相当于跳过了窗口降为1的过程】

# 2 HTTP/HTTPS

# 3 DNS

# 4 浏览器

# 5 网络攻击与安全

# 6 Ｑ＆Ａ
1. **什么是三次握手和四次挥手？**
    见1.2.2节。回答要点：数据包内容+客户端、服务端状态
2. **http和https是什么？有什么联系和区别？**
3. **在浏览器中输入url后到加载完整页面的过程？**
4. **常见的http状态码和含义？**
5. **跨域的解决方案？**
