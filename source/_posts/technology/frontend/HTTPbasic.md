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
端口号长度为16bit，范围0~65535，熟知端口号0~1023

FTP-21，TELNET-23，SMTP-25，DNS-53，HTTP-80，HTTPS-443

【套接字】IP:Port
ip地址和端口号唯一确定网络中的通信进程

### 1.2.1 UDP
无连接的非可靠传输协议，仅提供多路复用和对数据的错误检查两种服务。

主要用于对实时性有高要求的应用，包括**DNS**、TFTP、SNMP、RTP(实时传输协议)

UDP首部为固定的8B，包括源端口号、目的端口号、长度、校验和（校验和的计算请查看计网部分内容复习）

![UDP数据报格式]()

请注意，真实情况下UDP首部还会包括一个12B伪首部，所以udp数据报的真实结构：伪首部+首部+数据，这个伪首部实际上是ip数据报的首部

### 1.2.2 TCP
面向连接的可靠服务，不提供广播或者组播服务，包括确认、流量控制、拥塞管理等。

常见应用：FTP、**HTTP**、TELNET

TCP首部包含固定20B和可变部分

![TCP数据报格式]()

#### 1.2.2.1 建立连接-三次握手


#### 1.2.2.2 释放连接-四次握手

# 2 HTTP/HTTPS

# 3 DNS

# 4 浏览器

# 5 网络攻击与安全

# 6 Ｑ＆Ａ

