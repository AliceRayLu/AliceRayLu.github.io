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

#### 1.2.2.5 粘包问题

数据包头尾相连

#### 1.2.2.6 客户端与服务端建立长连接的方式

websocket：一次握手建立连接，全双工通信，服务器可以主动发送信息



#### 1.2.2.7 通过socket建立连接

# 2 HTTP/HTTPS
超文本传输协议，用于从服务器传输超文本内容给客户端浏览器

更加详细内容参考[这篇博客](https://blog.csdn.net/renxingzhadan/article/details/118946176)

## 2.1 HTTP请求和响应步骤

1. 客户端和服务端之间建立TCP连接
2. 客户端发送http请求（POST方法需要带上请求体）
3. 服务端接受请求并返回对应状态信息和数据
4. 释放TCP连接，除非要求connection keep alive
5. 浏览器解析并渲染

## 2.2 HTTP请求类型
| 方法 | 描述 |
|:--   | :-- |
| GET  | 请求指定页面信息，返回实体 |
| POST | 向指定资源提交数据处理请求，需要携带请求体|
| HEAD | 类似get请求，返回响应中没有具体内容，通常用于获取报头|
|DELETE| 请求服务器删除指定资源 |
| PUT  | 从客户端向服务器传送数据取代指定的内容 |
| TRACE| 回显服务器收到请求，用于测试或者诊断 |
|OPTIONS| 允许客户端查看服务器性能 |
|CONNECT| 将连接改为管道方式的代理服务器 |

【GET和POST的区别】
1. 浏览器回退表现不同：GET在浏览器回退时是无害的，而POST会再次提交请求（如表单等数据）
2. 浏览器对请求地址的处理不同：GET请求地址会被浏览器主动缓存，而POST不会，除非手动设置 
3. 浏览器对响应的处理不同：GET请求参数会被完整的保留在浏览器**历史记录**里，而POST中的参数不会被保留；GET请求获取的资源可以作为书签保存，POST不可以
4. **参数大小**不同：GET请求在URL中传送的参数是有长度的限制，而POST没有限制 
5. **安全性**不同. GET参数通过URL传递，会暴露，不安全；POST放在Request Body中，相对更安全 
6. 针对**数据操作**的类型不同：GET对数据进行查询，POST主要对数据进行增删改！简单说，GET是只读，POST是写。
7. 对参数的数据类型，GET只接受ASCII字符，而POST没有限制。

## 2.3 HTTP报文

### 2.3.1 请求报文
- 请求行：方法+URL+HTTP协议版本
- 请求头：每一行：一个头部字段名+值
- 空行
- 请求体：post携带的数据

```text
GET /sample.Jsp HTTP/1.1                               //请求行
Host  www.uuid.online/                                 //请求的目标域名和端口号
Origin  http://localhost:8081/                         //请求的来源域名和端口号 （跨域请求时，浏览器会自动带上这个头信息）
Referer  https://localhost:8081/link?query=xxxxx       //请求资源的完整URI
User-Agent  Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/67.0.3396.99 Safari/537.36       //浏览器信息
Cookie  BAIDUID=FA89F036:FG=1; BD_HOME=1; sugstore=0   //当前域名下的Cookie
Accept  text/html,image/apng                           //代表客户端希望接受的数据类型是html或者是png图片类型 
Accept-Encoding  gzip, deflate                         //代表客户端能支持gzip和deflate格式的压缩
Accept-Language  zh-CN,zh;q=0.9                        //代表客户端可以支持语言zh-CN或者zh(q(0~1)是优先级权重的意思，不写默认1，这里zh-CN是1，zh是0.9)
Connection  keep-alive                                 //告诉服务器，客户端需要的tcp连接是一个长连接
```

```text
POST / HTTP1.1
Host  www.wrox.com
User-Agent  Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 2.0.50727; .NET CLR 3.0.04506.648; .NET CLR 3.5.21022)
Content-Type  application/x-www-form-urlencoded
Content-Length  40
Connection  Keep-Alive
 
name=Professional%20Ajax&publisher=Wiley           //请求体数据行
```

### 2.3.2 响应报文
- 状态行
- 响应头
- 空行
- 响应体

```text
HTTP/1.1 200 OK                             //状态行
Date: Fri, 22 May 2009 06:07:21 GMT         //响应头
Content-Type: text/html; charset=UTF-8
 
<html>                                      //响应体（响应正文）
      <head></head>
      <body>
            <!--body goes here-->
      </body>
</html>
```
## 2.4 HTTP常见返回状态码
|状态码    |   含义                                     | 典型例子  |
| :--:    | :--                                         | :--    |
| 1xx     | 指示信息类，表示请求已接受，继续处理            |  **100**：继续请求 **101**：准备切换协议       |
| 2xx     | 指示成功类，表示请求已成功接受                  | **200**：请求成功 **201**: 成功创建资源  **204**: 成功处理请求但是没有返回          |
| 3xx     | 指示重定向，表示要完成请求必须进行更近一步的操作 | **301**：请求页面永久移动到新url **302**：请求页面临时移动 |
| 4xx     | 指示客户端错误，请求有语法错误或请求无法实现     | **403**：禁止，服务器拒绝请求  **404**：服务器找不到请求的网页   |
| 5xx      |指示服务器错误，服务器未能实现合法的请求         | **500**：服务器内部错误 **502**：错误网关  **503**：服务器不可用   |

## 2.5 HTTP跨域问题
### 2.5.1 基本概念
**【跨域】** 只要***协议**（http/https）*、***域名**（domin）*、***端口**（port）* 有任意一个不同就认为发生了跨域

**【浏览器同源策略】** 

阻止一个域的javascript脚本和另外一个域的内容进行交互，具体表现为：
1. 无法读取非同源网页的 Cookie、LocalStorage 和 IndexedDB
2. 无法接触非同源网页的 DOM
3. 无法向非同源地址发送 AJAX 请求

### 2.5.2 解决方案
避开浏览器的安全限制，参考[这篇博客](https://blog.csdn.net/qq_38128179/article/details/84956552)

- `JSONP`：通过`<script src>`标签发送请求
- `document.domin`：当主域名相同子域名不同时，可以通过设置两个页面相同的`document.domin`来实现两个页面共享cookie
- `window.name`：
- `window.postMessage()`：
    ```js
    // 父窗口打开一个子窗口
    var openWindow = window.open('http://test2.com', 'title');
 
    // 父窗口向子窗口发消息(第一个参数代表发送的内容，第二个参数代表接收消息窗口的url)
    openWindow.postMessage('Nice to meet you!', 'http://test2.com');
    ```
    ```js
    // 子窗口监听 message 消息
    window.addEventListener('message', function (e) {
        console.log(e.source); // e.source 发送消息的窗口
        console.log(e.origin); // e.origin 消息发向的网址
        console.log(e.data);   // e.data   发送的消息
    },false);
    ```
- `CORS`：开启跨域资源共享，允许通过的url
- `proxy`：nginx配置反向代理。原理：浏览器有同源策略，使用服务器向另一个服务器发送请求，然后将另一个服务器的响应返回客户端
- `websocket`：一种双向通信协议，允许客户端和服务器主动发送或接受数据（html5持久化协议）

## 2.6 HTTP和HTTPS联系与区别

- http 是超文本传输协议，信息是明文传输，https 则是具有安全性的**ssl加密传输**协议。
- https 协议需要 ca 证书，费用较高。
- 使用不同的链接方式，端口也不同，一般，http 协议的端口为 80，https 的端口为 443。
- http 的连接很简单，是无状态的；https有状态存储

## 2.7 HTTPS安全传输原理

- 收方能够证实发送方的真实身份
- 发送方事后不能否认所发送过的报文
- 收方或非法者不能伪造、篡改报文

### 2.7.1 非对称加密算法RSA

如果用公开密钥对数据进行加密，只有用对应的私有密钥才能解密。如果用私有密钥对数据进行加密，只有用对应的公开密钥才能解密。

公钥包括在数字证书中

### 2.7.2 SSL建立连接

## 2.8 HTTP各版本特性

### 2.8.1 HTTP 1.x
【1.0】

无状态，无连接

容易发生**队头阻塞**：下一个请求必须在前一个请求响应之后才能发送

使用头部的协商缓存、强缓存作为缓存的判断机制

不支持断点续传，每次都会传送完整的页面

明文传输，不安全

【1.1】
提供长连接

改进队头阻塞，使用管道机制，允许不受到应答就继续发送请求（没有解决发送方队头阻塞）

### 2.8.2 HTTP 2.x
使用https协议，提高安全性

对头部进行压缩，采用二进制传输，实现多路复用

允许服务端主动推送

### 2.8.3 HTTP 3.x
使用基于 UDP 的 QUIC 协议解决队头阻塞的问题

# 3 DNS & CDN
domin name system，域名解析系统，通过该系统将域名和ip地址一一对应

## 3.1 查询方式
本地域名服务器，根域名服务器，顶级域名服务器，权威域名服务器
- 递归查询：如果自己不知道，就自己发送一个请求到其他服务器，得到返回后再返回给请求的服务器
- 迭代查询：如果自己不知道，告诉请求的服务器如何去查找（向谁查找）

## 3.2 DNS缓存
- 浏览器缓存
- 操作系统缓存：存储在host文件中

## 3.3 从输入url到浏览器展示界面的过程

1. url解析
2. DNS查询
3. 建立tcp连接
4. Http请求&响应
5. 渲染页面:DOM树+CSS树 => render树

## 3.4 CDN
内容分发网络，根据距离用户最近的位置分配资源，用户在上网的时候不用直接访问源站，而是访问离他“最近的”一个 CDN 节点，术语叫边缘节点，其实就是缓存了源站内容的代理服务器。

应用CDN后，DNS 返回的不再是 IP 地址，而是一个CNAME(Canonical Name ) 别名记录，指向CDN的全局负载均衡

## 3.5 url组成
1. 协议
2. 域名
3. 端口号
4. 路径
5. 请求参数
6. 锚点

# 4 浏览器

## 4.1 cookie & sessionStorage & localStorage
都存储在客户端

- 数据大小：cookie大小不能超过4k，其他两个可以存储5M+大小的数据
- 有效时间：cookie在有效期结束之前一直有效，localStorage永久有效（除非手动删除），sessionStorage在浏览器窗口关闭前有效（关闭后自动删除）
- 数据存储：cookie会被传输至服务端，local和session只存储在本地

cookie

## 4.2 缓存机制

### 4.2.1 强制缓存
浏览器缓存结果和缓存标识都存在，查找请求结果，根据缓存规则决定是否使用缓存

### 4.2.2 协商缓存
强制缓存失效，浏览器携带本地缓存标识询问服务器是否使用缓存。

### 4.2.3 优先使用

## 4.3 严格模式和混杂模式

## 4.4 浏览器进程和线程

关于同步、异步问题，事件循环等内容

- 浏览器主进程（一个），浏览器tab切换、回退刷新等操作
- 网络进程，负责网络资源加载（一个）
- GPU进程（一个），负责像素点绘制
- 插件进程（一个插件一个）
- 渲染进程（一个tab一个），多个tab互不影响：渲染进程中有多个线程
    - GUI渲染线程
    - JS引擎线程
    - 事件触发线程
    - 异步请求线程
    - 定时触发器线程

在浏览器中打开一个网页相当于新起了一个进程（进程内有自己的多线程）

线程之间关系：gui和js互斥

# 5 网络攻击与安全

## 5.1 xss攻击
跨站脚本攻击，允许攻击者将恶意代码植入到提供给其它用户使用的页面中

注入恶意sql语句 劫持cookie

【解决方案】
在使用 .innerHTML、.outerHTML、document.write() 时要特别小心，不要把不可信的数据作为 HTML 插到页面上，而应尽量使用 .textContent、.setAttribute() 等

## 5.2 csrf攻击
攻击者诱导受害者进入第三方网站，在第三方网站中，向被攻击网站发送跨站请求

【解决方案】
- 阻止不明外域的访问
- 要求提供token或双重cookie验证

## 5.3 ddos攻击

## 5.4 sql注入攻击
将恶意的 Sql查询或添加语句插入到应用的输入参数中，再在后台 Sql服务器上解析执行进行的攻击

【解决方案】
- 严格检查输入变量的类型和格式
- 过滤和转义特殊字符
- 对访问数据库的Web应用程序采用Web应用防火墙


# 6 Ｑ＆Ａ
1. **什么是三次握手和四次挥手？**
    见1.2.2节。回答要点：数据包内容+客户端、服务端状态
2. **http和https是什么？有什么联系和区别？**
    http和https是超文本传输协议，联系与区别见2.6节
3. **在浏览器中输入url后到加载完整页面的过程？**
    见3节
4. **常见的http状态码和含义？**
    见2.4节
5. **跨域的解决方案？**
    见2.5节，浏览器同源策略以及避开安全限制的方法
