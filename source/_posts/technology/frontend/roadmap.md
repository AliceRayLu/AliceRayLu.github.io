---
title: 【前端八股】Roadmap
date: 2024-01-19
category: [Technology,Frontend]
---

参考与详细的路线图：[🔗frontend roadmap](https://roadmap.sh/frontend)

- Internet & browser
- HTML
- CSS
- JavaScript
- Frameworks
- git

以上是本人整理的部分材料，也参考了很多网上的资料，以下是完整的参考资料：

- [前端八股大全](https://vue3js.cn/interview/)：这一份比较粗浅，适合快速阅读理清关键知识点主干，建议前期上手时阅读
- [详细八股](https://juejin.cn/post/6959043611161952269)：这位作者的全系列非常详细，特别是手写题和浏览器原理题写的特别好
- [前端性能优化](https://juejin.cn/post/7029973323475845150)：问项目的时候很喜欢问一些可以优化的点以及复盘

## Network

---
title: 【前端八股】计算机网络
date: 2024-01-14
category: [Technology,Frontend]
toc_number: false
---

### 1 网络工作原理

#### 1.1 网络模型
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



#### 1.2 传输层
- 传输层提供**端到端**的通信，即进程和进程之间的通信。（端口标识进程）
- 传输层需要对报文进行差错检测
- 提供TCP和UDP两种不同的传输协议 

【端口】
端口号长度为16bit，范围0-65535，熟知端口号0-1023

FTP-21，TELNET-23，SMTP-25，DNS-53，HTTP-80，HTTPS-443

【套接字】IP:Port
ip地址和端口号唯一确定网络中的通信进程

##### 1.2.1 UDP
user data protocol-无连接的非可靠传输协议，仅提供多路复用和对数据的错误检查两种服务。

主要用于对实时性有高要求的应用，包括**DNS**、TFTP、SNMP、RTP(实时传输协议)

UDP首部为固定的8B，包括源端口号、目的端口号、长度、校验和（校验和的计算请查看计网部分内容复习）

![UDP数据报格式](https://github.com/AliceRayLu/AliceRayLu.github.io/blob/main/source/_posts/technology/frontend/assets/udp.png?raw=true)

请注意，真实情况下UDP首部还会包括一个12B伪首部，所以udp数据报的真实结构：伪首部+首部+数据，这个伪首部实际上是ip数据报的首部

##### 1.2.2 TCP
transmission control protocol-面向连接的可靠服务，不提供广播或者组播服务，包括确认、流量控制、拥塞管理等。

常见应用：FTP、**HTTP**、TELNET

TCP首部包含固定20B和可变部分

![TCP数据报格式](https://github.com/AliceRayLu/AliceRayLu.github.io/blob/main/source/_posts/technology/frontend/assets/tcp.png?raw=true)

###### 1.2.2.1 建立连接-三次握手
![三次握手](https://github.com/AliceRayLu/AliceRayLu.github.io/blob/main/source/_posts/technology/frontend/assets/3shake.png?raw=true)

1. 客户端发送带SYN标志的数据包，发送一个随机序列号
2. 接收端/服务端收到后返回带有SYN和ACK标志的数据包，确认收到的序列号(ack=x+1)并发送自己的SYN包(seq=y)
3. 客户端向服务端发送确认包，两者都进入established状态开始传输数据


###### 1.2.2.2 释放连接-四次挥手
![四次挥手](https://github.com/AliceRayLu/AliceRayLu.github.io/blob/main/source/_posts/technology/frontend/assets/4shake.png?raw=true)

1. 客户端发送带FIN标志的数据包以及当前传输数据序列号
2. 服务端向客户端发送ACK确认数据包，并将剩余数据继续传输
3. 服务端将所有数据传输完毕后，向客户端发送FIN和ACK数据包
4. 客户端收到报文后发送确认数据报，服务端接收后进入closed状态，客户端在等待2*MSL（最长报文段寿命）后进入closed状态

客户端和服务端的任何一方都可以主动发起释放连接的请求

###### 1.2.2.3 重传
超时和冗余ACK会触发TCP重传
- **超时**：对每个发送报文段设置一个计时器，重传时间到期但是未收到确认就要自动重传。
- **冗余ACK**：发送方收到了两次某个报文段的ACK，通常在比当前期望的序号大的报文到达时，再次发送前面已经接收到的报文序列ACK

###### 1.2.2.4 流量控制
基于滑动窗口协议控制流量，确认报文携带允许传输的窗口大小，进行端到端的调整

###### 1.2.2.5 拥塞控制
拥塞控制一共有4种算法：
- **慢开始**：将发送方的拥塞窗口先置为1（一个最大报文段长度），收到确认后逐步增大拥塞窗口（加倍：1->2, 2->4）
    在慢开始达到了规定阈值后，改用拥塞避免算法
- **拥塞避免**：每经过一个往返时延RTT将拥塞窗口加1，出现拥塞时（未按时收到确认），将拥塞窗口重新设为1，重新执行慢开始算法（慢开始阈值改为一半？）
- **快重传**：通过发送冗余ACK包的方式来触发重传
- **快恢复**：把慢开始的阈值设为当前窗口大小的一半，然后使用拥塞避免算法将窗口缓慢增大（逐步加1）。【相当于跳过了窗口降为1的过程】

###### 1.2.2.5 粘包问题

数据包头尾相连

###### 1.2.2.6 客户端与服务端建立长连接的方式

websocket：一次握手建立连接，全双工通信，服务器可以主动发送信息



###### 1.2.2.7 通过socket建立连接

### 2 HTTP/HTTPS
超文本传输协议，用于从服务器传输超文本内容给客户端浏览器

更加详细内容参考[这篇博客](https://blog.csdn.net/renxingzhadan/article/details/118946176)

#### 2.1 HTTP请求和响应步骤

1. 客户端和服务端之间建立TCP连接
2. 客户端发送http请求（POST方法需要带上请求体）
3. 服务端接受请求并返回对应状态信息和数据
4. 释放TCP连接，除非要求connection keep alive
5. 浏览器解析并渲染

#### 2.2 HTTP请求类型
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

#### 2.3 HTTP报文

##### 2.3.1 请求报文
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

##### 2.3.2 响应报文
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
#### 2.4 HTTP常见返回状态码
|状态码    |   含义                                     | 典型例子  |
| :--:    | :--                                         | :--    |
| 1xx     | 指示信息类，表示请求已接受，继续处理            |  **100**：继续请求 **101**：准备切换协议       |
| 2xx     | 指示成功类，表示请求已成功接受                  | **200**：请求成功 **201**: 成功创建资源  **204**: 成功处理请求但是没有返回          |
| 3xx     | 指示重定向，表示要完成请求必须进行更近一步的操作 | **301**：请求页面永久移动到新url **302**：请求页面临时移动 |
| 4xx     | 指示客户端错误，请求有语法错误或请求无法实现     | **403**：禁止，服务器拒绝请求  **404**：服务器找不到请求的网页   |
| 5xx      |指示服务器错误，服务器未能实现合法的请求         | **500**：服务器内部错误 **502**：错误网关  **503**：服务器不可用   |

#### 2.5 HTTP跨域问题
##### 2.5.1 基本概念
**【跨域】** 只要***协议**（http/https）*、***域名**（domin）*、***端口**（port）* 有任意一个不同就认为发生了跨域

**【浏览器同源策略】** 

阻止一个域的javascript脚本和另外一个域的内容进行交互，具体表现为：
1. 无法读取非同源网页的 Cookie、LocalStorage 和 IndexedDB
2. 无法接触非同源网页的 DOM
3. 无法向非同源地址发送 AJAX 请求

##### 2.5.2 解决方案
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
- `CORS`：开启跨域资源共享，允许通过的url（使用额外的 HTTP 头来告诉浏览器  让运行在一个 origin (domain)上的Web应用被准许访问来自不同源服务器上的指定的资源）
- `proxy`：nginx配置反向代理。原理：浏览器有同源策略，使用服务器向另一个服务器发送请求，然后将另一个服务器的响应返回客户端
- `websocket`：一种双向通信协议，允许客户端和服务器主动发送或接受数据（html5持久化协议）

#### 2.6 HTTP和HTTPS联系与区别

- http 是超文本传输协议，信息是明文传输，https 则是具有安全性的**ssl加密传输**协议。
- https 协议需要 ca 证书，费用较高。
- 使用不同的链接方式，端口也不同，一般，http 协议的端口为 80，https 的端口为 443。
- http 的连接很简单，是无状态的；https有状态存储

#### 2.7 HTTPS安全传输原理

- 收方能够证实发送方的真实身份
- 发送方事后不能否认所发送过的报文
- 收方或非法者不能伪造、篡改报文

##### 2.7.1 非对称加密算法RSA

如果用公开密钥对数据进行加密，只有用对应的私有密钥才能解密。如果用私有密钥对数据进行加密，只有用对应的公开密钥才能解密。

公钥包括在数字证书中

##### 2.7.2 SSL建立连接

正常三次握手的过程中发送：
1. 支持的加密算法
2. SSL协议版本和需要访问的域名
3. 一个随机数

服务器返回：
1. 选中的加密算法
2. SSL、TLS协议版本
3. 第二个随机数

【证书验证阶段-使用非对称加密】

服务器端发送证书和公钥

【后续数据传输过程持续使用对称加密】

#### 2.8 HTTP各版本特性

##### 2.8.1 HTTP 1.x
【1.0】

无状态，无连接

容易发生**队头阻塞**：下一个请求必须在前一个请求响应之后才能发送

使用头部的协商缓存、强缓存作为缓存的判断机制

不支持断点续传，每次都会传送完整的页面

明文传输，不安全

【1.1】
提供长连接

引入etag增强缓存机制

改进队头阻塞，使用管道机制，允许不受到应答就继续发送请求（没有解决发送方队头阻塞）

支持断点续传

##### 2.8.2 HTTP 2.x
使用https协议，提高安全性

对头部进行压缩，采用二进制传输，实现多路复用

允许服务端主动推送

##### 2.8.3 HTTP 3.x
使用基于 UDP 的 QUIC 协议解决队头阻塞的问题

### 3 DNS & CDN
domin name system，域名解析系统，通过该系统将域名和ip地址一一对应

#### 3.1 查询方式
本地域名服务器，根域名服务器，顶级域名服务器，权威域名服务器
- 递归查询：如果自己不知道，就自己发送一个请求到其他服务器，得到返回后再返回给请求的服务器
- 迭代查询：如果自己不知道，告诉请求的服务器如何去查找（向谁查找）

#### 3.2 DNS缓存
- 浏览器缓存
- 操作系统缓存：存储在host文件中

#### 3.3 从输入url到浏览器展示界面的过程

1. url解析
2. DNS查询
3. 建立tcp连接
4. Http请求&响应
5. 渲染页面:DOM树+CSS树 => render树

#### 3.4 CDN
内容分发网络，根据距离用户最近的位置分配资源，用户在上网的时候不用直接访问源站，而是访问离他“最近的”一个 CDN 节点，术语叫边缘节点，其实就是缓存了源站内容的代理服务器。

应用CDN后，DNS 返回的不再是 IP 地址，而是一个CNAME(Canonical Name ) 别名记录，指向CDN的全局负载均衡

#### 3.5 url组成
1. 协议
2. 域名
3. 端口号
4. 路径
5. 请求参数
6. 锚点

### 4 浏览器

#### 4.1 cookie & sessionStorage & localStorage
都存储在客户端

- 数据大小：cookie大小不能超过4k，其他两个可以存储5M+大小的数据
- 有效时间：cookie在有效期结束之前一直有效，localStorage永久有效（除非手动删除），sessionStorage在浏览器窗口关闭前有效（关闭后自动删除）
- 数据存储：cookie会被传输至服务端，local和session只存储在本地

详情查看js篇

#### 4.2 缓存机制

##### 4.2.1 强制缓存
浏览器缓存结果和缓存标识都存在，查找请求结果，根据缓存规则决定是否使用缓存

##### 4.2.2 协商缓存
强制缓存失效，浏览器携带本地缓存标识询问服务器是否使用缓存。

命中协商缓存返回304

##### 4.2.3 优先使用
先根据cache-control查询是否超过了有效期时间，没有超过使用强制缓存；

超过则向服务器发送请求询问是否使用缓存，服务器比较etag，返回更新的资源

【etag和last-modified】

last-modified保存上一次更新的时间，etag保存hash

last-modified只精确到秒级，并且依赖于文件修改时间，不够准确

【刷新】

刷新会导致本地文件强制过期，如果在地址栏输入url则按照正常流程查询是否过期

#### 4.3 严格模式和混杂模式

#### 4.4 浏览器进程和线程

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

### 5 网络攻击与安全

#### 5.1 xss攻击
跨站脚本攻击，允许攻击者将恶意代码植入到提供给其它用户使用的页面中

注入恶意sql语句 劫持cookie

【解决方案】
在使用 .innerHTML、.outerHTML、document.write() 时要特别小心，不要把不可信的数据作为 HTML 插到页面上，而应尽量使用 .textContent、.setAttribute() 等

#### 5.2 csrf攻击
攻击者诱导受害者进入第三方网站，在第三方网站中，向被攻击网站发送跨站请求

【解决方案】
- 阻止不明外域的访问
- 要求提供token或双重cookie验证

#### 5.3 ddos攻击

#### 5.4 sql注入攻击
将恶意的 Sql查询或添加语句插入到应用的输入参数中，再在后台 Sql服务器上解析执行进行的攻击

【解决方案】
- 严格检查输入变量的类型和格式
- 过滤和转义特殊字符
- 对访问数据库的Web应用程序采用Web应用防火墙


### 6 Ｑ＆Ａ
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

----

## HTML


# 1 HTML5新特性
- 加入语义化标签
- 加入媒体标签：`audio, video`
- 表单form
- dom查询操作：`querySelector`
- web存储:localStorage, sessionStorage
- 其他：draggable

# 2 语义化标签

- `<header></header>`  头部
- `<nav></nav>`  导航栏
- `<section></section>`  区块（有语义化的div）
- `<main></main>`  主要区域
- `<article></article>`  主要内容
- `<aside></aside>`  侧边栏
- `<footer></footer>`  底部


# 3 块级元素与行内元素

## 3.1 块级元素
- div：容器
- dl：html5之前用于定义列表，与`<dt>`（子条目标题）和`<dd>`（子条目内容）嵌套使用
    ```html
    <dl>
        <dt>Beast of Bodmin</dt>
        <dd>A large feline inhabiting Bodmin Moor.</dd>

        <dt>Morgawr</dt>
        <dd>A sea serpent.</dd>
    </dl>
    ```
- form 
- h1 h2 h3 h4 h5 h6 
- hr 
- ol li p pre table td tr

## 3.2 行内元素

a b s i u span br img input textarea sub sup

## 3.3 行内与块级元素的区别

行内元素：
1. 无法设置宽高；
2. 对margin仅设置左右有效，上下无效；
3. padding上下左右有效；不会自动换行

块级元素：
1. 可以设置宽高
2. margin和padding的上下左右均对其有效
3. 超出当前行会自动换行
4. 多个块状元素标签写在一起，默认排列方式为从上至下

# 4 标签中嵌入
使用`&lt;`在标签中使用尖角符号
```html
<p> 这是被&lt;p&gt;包含起来的内容</p>
```

----
## CSS

# 1 CSS选择器

id选择器（#box），选择id为box的元素

类选择器（.one），选择类名为one的所有元素

标签选择器（div），选择标签为div的所有元素

后代选择器（#box div），选择id为box元素内部所有的div元素

子选择器（.one>one_1），选择父元素为.one的所有.one_1的元素

相邻同胞选择器（.one+.two），选择紧接在.one之后的所有.two元素

群组选择器（div,p），选择div、p的所有元素

## 1.1 选择器优先级

内联 > id选择器 > 类选择器 > 标签选择器

## 1.2 复合选择器

# 2 预处理器
less sass

# 3 CSS3新特性

# 4 盒模型

## 4.1 标准盒模型与IE盒模型

标准盒模型的宽度以及高度只计算实际内容content的宽高，IE盒模型的宽高是除了margin之外所有border（包含）以内的元素宽高

使用box-sizing属性改变盒模型类型，默认为标准

```css
box-sizing: border-box; /* 使用ie盒模型 */
```

## 4.2 居中对齐

### 4.2.1 水平居中

### 4.2.2 垂直居中

# 5 像素大小

## 5.1 px

## 5.2 em/rem

## 5.3 vw/vh

# 6 position

- `relative`：相对于默认位置的偏移
- `absolute`：相对于父级元素的偏移
- `fixed`：相对于浏览器窗口是固定的位置

absolute和fixed会脱离文档流

# 7 布局

## 7.1 两栏布局

- 设置左侧固定宽度，float:left，右栏使用margin-left撑出空间
- 使用flex布局：父元素使用display：flex，左边栏固定宽度，右边栏flex：1

## 7.2 三栏布局
- 两边使用 float，中间使用 margin
- 两边使用 absolute，中间使用 margin
- display: table 实现
- flex实现
- grid网格布局

## 7.3 grid布局

## 7.4 flex

flex-direction

### 7.4.1 flex:1;
- flex-grow:1; 将该行多余的空间按比例分给这个元素
- flex-shrink:1; 超出部分按比例分配到每个元素进行挤压
- flex-basis: 0%; 计算多余空间

## 7.5 BFC

## 7.6 文字溢出

# 8 回流与重绘

回流：布局引擎会根据各种样式计算每个盒子在页面上的大小与位置

重绘：当计算好盒模型的位置、大小及其他属性后，浏览器根据每个盒子特性进行绘制

# 9 动画

## transition

【包含属性】
- transition-property
- transition-duration
- transition-timing-function
- transition-delay

## transform

使用transform来改变元素位置属性，不会像position那样触发回流（重新布局计算），可以优化性能。

## translate

## animation

# 10 性能优化

# 11 CSS兼容不同浏览器

## Javascript

# 1 数据类型

## 1.1 let/const/var
用于声明变量

- `var`：函数作用域，存在提升现象，在全局定义时会变成window对象的属性
- `let`：块作用域，作用域更小，不允许冗余（重复）声明
- `const`：const基本与let相同，但是声明时必须初始化且不能修改（如果const指向一个对象，可以修改对象内部属性值）

【var/let迭代变量现象】
```js
for(var i = 0;i < 5;++i){
    setTimeout(() => console.log(i),0) // 输出5,5,5,5,5
}

for(let i = 0;i < 5;++i){
    setTimeout(() => console.log(i),0) // 输出0,1,2,3,4
}
```

## 1.2 基本数据类型

- `Undefined`
- `Null`：表示一个空对象指针
- `Boolean`
- `Number`：8进制-0o______，16进制-0x____，浮点数（IEEE754），科学计数法（e）
- `String`：string类型不可变
- `Symbol`(ES6新增)

以上是6种基本数据类型，以下是引用数据类型。

- `Object`
- `Array`
- `Function`

基本数据类型存储在栈中，直接存储对应值，引用数据类型存储在堆中，在栈中存放关于这个对象的引用。

### 1.2.1 undefined
声明但是没有初始化

请注意**未声明报错**和undefined区别

```js
let mess = undefined // 显式undefined初始化（不必要：默认）
console.log(mess == undefined) //true

if(mess){
    //不执行
}
if(!mess) // 执行

console.log(null == undefined) // true
console.log(null === undefined) // false
```

【null VS undefined】
使用null初始化空值，undefined表明未定义。undefined从null中派生，null是指向空对象的引用。

### 1.2.2 boolean
`true`和`false`区分大小写，只有全小写是bool值，其他形式都是标识符。

【其他类型布尔值等价形式】
| true            |          false|
| :--:            |     :--:      |
| 非空string      | ""(empty string) |
|非零数值         | 0，NaN           |
| 任意对象         | null          |
| N/A(不存在)      | undefined      |


### 1.2.3 NaN
Nan任何操作始终返回NaN
```js
console.log(NaN == NaN) // false
isNaN(NaN) // true
isNaN(10) // false
isNaN("10") //false，可以转化为数值
isNaN("blue") // true 不可以转化为数值
isNaN(true) // false 可以转化为1
```

### 1.2.4 string操作

#### 1.2.4.1 模板字符串
`包括的字符串是模板字符串，允许**换行**，**嵌入变量**
```js
let val = `hi
hither`;
let jas = `${val} use`
```

#### 1.2.4.2 修改
- `+`/`concat()`/`${}`都可以用于拼接字符串
- `slice(start,end)`/`substring(start,end)`：获取[start,end)副本
- `substr(start,len)`：获取从start开始长度为len的字符串副本
- `trim()`/`trimLeft()`/`trimRight()`：删除指定位置空格
- `repeat(n)`：字符串重复n次
- `padStart(len,char)`/`padEnd(len,char)`：当字符串长度不满len时，使用char填充到指定位置
- `toLowerCase()`/`toUpperCase()`：全小写，全大写

#### 1.2.4.3 查询
- `charAt(pos)`
- `indexOf(string)`
- `startWith(string)`
- `includes(string)`

#### 1.2.4.4 正则表达式匹配
基于正则表达式
- `match(pattern)`：返回一个匹配的字符串数组
- `search(pattern)`：返回找到的位置下标
- `replace(old,new)`：替换字符串中匹配的位置，返回替换后的结果字符串

#### 1.2.4.5 转化
- `split(char)`：按照char分割字符串，返回字符串数组

### 1.2.5 Object常用方法
- `Object.assign(obj,src1,src2,...)`：后面的src会覆盖前面src的相同属性
- `Object.create(proto)`：创建一个以proto为原型的对象
- `Object.entries(obj)`：可枚举属性对数组
- `Object.keys(obj)`：自身可枚举属性（不包括原型链）【`for...in`：全部可枚举属性，包括原型链】
- `Object.getOwnPropertyNames(obj)`：自身所有属性，包括可枚举不可枚举（不包括原型链）
- `Object.values(obj)`：与keys对应

### 1.2.6 Symbol
用于标记唯一对象，不可以使用`new Symbol()`

【创建方法】
- `const s = Symbol("foo")`这种方法创建的即便描述一样也会被认为是不同的symbol
- `const s = Symbol.for("foo")`这种方法创建的会注册在全局symbol表中，相同的描述会被视为同一个

【应用】
- 程序中的唯一标识符（代替状态常量）
- 类中私有属性/方法，不会被外部api访问

## 1.3 类型转换
- Number()
- parseInt() / parseInt(object,base)[指定底数]
- parseFloat()
- toString() / toString(base)[数值转换字符串指定底数]
- valueOf()
- String()

### 1.3.1 显式类型转换
明确调用某些方法：
- Number()
- parseInt()
- String()
- Boolean()


### 1.3.2 隐式类型转换

- 比较运算（==、!=、>、<）、if、while需要布尔值地方
- 算术运算（+、-、*、/、%）


## 1.4 相等性比较与拷贝

### 1.4.1 == 与 ===
两边类型不同的时候，`==`会先进行类型转换再进行比较，但是`===`会同时检查类型和值

`Object.is(a,b)`行为基本上与`===`一致，除了正负0判断和NaN判断

```js
+0 === -0;           // true
Object.is(+0, -0)    // false

NaN === NaN          // false
Object.is(NaN, NaN)  // true
```

### 1.4.2 深拷贝和浅拷贝

#### 1.4.2.1 浅拷贝
拷贝时只拷贝一层，即基本类型拷贝一份精确复制，对于引用对象类型拷贝一份内存地址，深层的引用共享相同的内存地址。

```js
function shallowCopy(obj){
    var newobj = {};
    for(let prop in obj){
        if(obj.hasOwnProperty(prop)){
            newobj[prop] = obj[prop];
        }
    }
    return newobj;
}
```

【存在浅拷贝现象的方法】
- `Object.assign`：将源对象赋值合并给目标对象，并返回合并后目标对象的值
    ```js
    Object.assign(target, ...sources)
    ```
- `Array.prototype.slice()`, `Array.prototype.concat()`
- 使用拓展运算符实现的复制
    ```js
    let arr = [1,2,3];
    let narr = [...arr];
    narr[1] = 5;
    console.log(narr);
    console.log(arr);
    ```

#### 1.4.2.2 深拷贝
开辟一个栈，把所有属性都严格拷贝一份。因此改变一个对象的属性值不会影响另一个对象的属性值。

【实现方式】

- `_.cloneDeep()`
    ```js
    const _ = require('lodash');
    const obj1 = {
        //属性
    };
    const obj2 = _.cloneDeep(obj1);
    ```
- `jQuery.extend()`
- `Json.stringify()`
- 手写
    ```js
    function deepCopy(obj){
        //只拷贝对象
        if(!obj || typeof obj !== 'object')return;
        let newobj = Array.isArray(obj)?[]:{};
        for(let prop in obj){
            if(obj.hasOwnProperty(prop)){
                newobj = (typeof obj[prop] === 'object')?deepCopy(obj[prop]):obj[prop];
            }
        }
        return newobj;
    }
    ```


## 1.5 判断数据类型

### 1.5.1 typeof
typeof会返回以下字符串：
- `undefined`
- `boolean`
- `number`
- `string`
- `object`
- `function`：函数理论上是一种特殊的对象，但是要区分函数和普通对象，因此有function
- `symbol`

`typeof null`会返回object，认为null是一个对空对象的引用 

typeof是**操作符**而不是函数，不需要参数，可以使用参数。

```js
let message = "ssss";
console.log(typeof message); // string
console.log(typeof(message)) // string
console.log(typeof 95) // number

typeof {} // object
typeof [] // object
```

【手写typeof】
```js
function typeof(obj){
    return Object.prototype.toString.call(obj).slice(8,-1).toLowerCase();
}
```

### 1.5.2 instanceof
instanceof 运算符用于检测构造函数的 prototype 属性是否出现在某个实例对象的原型链上

一般格式为`object instanceof constructor`

```js
let Car = function() {}
let benz = new Car()
benz instanceof Car // true
let car = new String('xxx')
car instanceof String // true
let str = 'xxx'
str instanceof String // false
```

实现原理：在原型链上依次查找是否由该constructor构建

```js
function instanceOf(left,right){
    if(left === null || typeof left != "object")return false;
    let proto = Object.getPrototypeOf(left);
    while(proto != null){
        if(proto == right.prototype) return true;
        proto = Object.getPrototypeOf(proto);
    }
    return false;
}
```

【typeof和instanceof的区别】
- typeof返回字符串，告知对象类型，instanceof返回布尔值
- instanceof用于判断引用对象类型，不能用于判断基础数据类型
- typeof用于判断基础数据类型和function引用对象类型，无法判断具体的复杂引用对象类型

### 1.5.3 通用检测
通用方法：`Object.prototype.toString()`

【手写通用检测方法】
```js
function getType(obj){
    let type = typeof obj;
    if(type != "object")return type;
    return Object.prototype.toString.call(obj).replace(/^\[object (\S+)\]$/,'$1');
}
```

# 2 数据结构
## 2.1 set
- `add(a)`
- `delete(a)`
- `has(a)`
- `clear()`
keys()：返回键名的遍历器
values()：返回键值的遍历器
entries()：返回键值对的遍历器
forEach()：使用回调函数遍历每个成员

### weakset

## 2.2 map
size 属性
set(key,value)
get()
has()
delete()
clear()

### weakmap

## 2.3 json

## 2.4 array

### 2.4.1 数组修改操作
- `push(a,b,...)`：在末尾追加任意多个值
- `unshift(a,b,...)`：在开头插入任意多个值（开头保持unshift参数顺序）
- `concat(a,b,...)`：将数组拼接在一起，返回拼接后的新数组，不影响原来的数组
- `pop()`：删除数组的最后一项
- `shift()`：删除数组的第一项

【splice和slice】
- `slice(start,end)`：对原数组不产生影响，返回[start,end)这一段的数组，如果不指定end，默认到数组结尾
- `splice(start,len,a,b,...)`：对原数组产生影响，从start位置开始，删除掉len个元素，然后在该位置继续插入后续的元素。返回被移除的元素数组。

### 2.4.2 数组查询操作
- `indexOf(a)`：返回某个数的下标，如果不存在返回-1
- `includes(a)`：是否包含某个元素，返回true/false
- `find(func)`：返回满足func的第一个元素
    ```js
    let arr = [1,2,43,24];
    arr.find((el)=>el > 28);
    ```

### 2.4.3 排序
- `reverse()`：对数组进行翻转
- `sort(func)`：按照提供的规则进行函数排序
    ```js
    function cmp(value1,value2){
        if(value1 < value2){
            return -1;
        }else if(value1 > value2){
            return 1;
        }else{
            return 0;
        }
    }
    ```

### 2.4.4 遍历

- `some(func)`：如果有元素满足func条件，返回true
- `every(func)`：如果所有元素满足func条件，返回true
- `forEach(func)`：对每一个元素运行函数，没有返回值
- `filter(func)`：返回满足筛选函数的数组
- `map(func)`：返回每个函数经过func操作后的数组

对于数组遍历，`for in`绑定下标，`for of`才是绑定元素

### 2.4.5 Array.prototype方法重写

#### 2.4.5.1 flat

```js
Array.prototype.flat = function(deep = 1) {
    let res = [];
    deep--;
    for(const val of this){
        if(Array.isArray(val) && deep >= 0){
            res = res.concat(val.flat(deep));
        }else{
            res.push(val);
        }
    }
    return res;
}
```

#### 2.4.5.2 map
```js
Array.prototype.map = function(callback){
    let res = [];
    for(let i = 0;i < this.length;i++){
        res.push(callback(this[i],i,this));
    }
    return res;
}
```

# 3 control flow

## 3.1 loops & iterators

### for in VS for of

for in 遍历对象中所有属性，包括原型属性。如果是数组的话按照index遍历

for of 遍历数组元素值，不能遍历对象

## 3.2 branches

# 4 函数

## 4.1 普通函数和箭头函数
- 箭头函数都是匿名函数，普通函数可以是匿名函数
- 箭头函数不能用于构造器，不能用于new
- 箭头函数没有this，箭头函数中的this都指向函数上下文，使用call，bind，apply也没有办法改变指向
- 箭头函数中不含有arguments形参数组，但是可以使用上下文中的形参数组

## 4.2 参数

### 4.2.1 剩余参数
使用`...`，将传入不定数量的元素集合成一个数组
```js
function func(v1,v2,...arr){

}
```

剩余参数必须是最后一个参数。

### 4.2.2 arguments数组
arguments和函数的参数同步，修改函数参数值就是修改arguments对应元素。

如果不传参，默认为undefined


## 4.3 闭包

一个函数被其引用的状态包围在一起，函数被引用包围

### 4.3.1 优缺点

【优点】保护函数内变量的安全，封装降低耦合

【缺点】容易造成内存泄漏，内存浪费问题

### 4.3.2 适用场景
- 设计一些私有方法和变量
- 延长变量的生命周期

```js
// 柯里化函数

function getArea(width){
    return height => {
        return width * height;
    }
}
let getAreaByTen = getArea(10);
console.log(getAreaByTen(20));
```

```js
// 封装一个计数器counter
var Counter = (function(){
    var privateCount = 0;
    function changeBy(val){
        privateCount += val;
    }
    return {
        increment:function(){
            changeBy(1);
        },
        decrement:function(){
            changeBy(-1);
        },
        value:function(){
            return privateCount;
        }
    }
})

let count1 = Counter();
count1.increment();
count1.increment();
console.log(count1.value()); // 2
```

## 4.4 作用域
块级，函数级，全局作用域级

【作用域链】
从最内部的块级/函数级作用域开始，向外部寻找

# 5 事件

## 5.1 事件与事件流
javascript中的事件，可以理解就是在HTML文档或者浏览器中发生的一种交互操作，使得网页具备互动性， 常见的有加载事件、鼠标事件、自定义事件等

包括事件和事件流。事件流的产生是因为父子结点执行事件存在顺序问题。

【事件流的三个阶段】
1. 事件捕获阶段(capture phase)
2. 处于目标阶段(target phase)/事件处理阶段
3. 事件冒泡阶段(bubbling phase)：从子节点依次上传直到DOM根节点

## 5.2 事件模型

- 原始事件模型（DOM0级）：标签/js直接绑定，绑定速度快，支持冒泡不支持捕获，不能重复绑定（只能绑定一次）
- 标准事件模型（DOM2级）：事件流
    ```js
    var btn = document.getElementById('.btn');
    btn.addEventListener(‘click’, showMessage, false);
    btn.removeEventListener(‘click’, showMessage, false);
    ```
    - 允许绑定多个事件处理器
    - 第三个参数设为true，允许捕获阶段执行，false冒泡阶段执行
- IE事件模型（基本不用）：只有事件处理阶段和冒泡阶段

## 5.3 事件循环
任务分为同步任务和异步任务。

同步任务进入主线程，即主执行栈，异步任务进入任务队列，主线程内的任务执行完毕为空，会去任务队列读取对应的任务，推入主线程执行。


[事件循环详解](https://juejin.cn/post/7020710294083092493)

### 5.3.1 微任务和宏任务

异步任务划分为宏任务和微任务。以下宏任务和微任务的划分是在浏览器中的划分，node.js的划分是不同的。

【宏任务】
- `setTimeout()`
- `setInterval()`

【微任务】
- `promise.then()`
- `async/await`
- `new MutationObserver()`

同步任务执行完毕后，会先查看微任务队列，当微任务队列执行完毕后才会去查看调用宏任务队列。

### 5.3.2 async & await
async就是用来声明一个异步方法，而 await是用来等待异步方法执行

await相当于生成一个promise，await紧接的内容放入promise中，进入微任务队列，而await语句后的语句被阻塞，相当于放入了promise.then的微任务队列。


#### 5.3.2.1 async
async函数返回一个promise对象
```js
function f() {
    return Promise.resolve('TEST');
}

// asyncF is equivalent to f!
async function asyncF() {
    return 'TEST';
}
```
#### 5.3.2.2 await
await后面接一个promise对象，返回这个对象的结果

## 5.4 异步&promise

### 5.4.1 promise状态
- pending（进行中）
- fulfilled（已成功）
- rejected（已失败）

### 5.4.2 promise方法
【promise.all】

并发同时开始执行promise序列，只有全部成功返回全部的成功信息数组，否则被catch捕获error


一些异步的结果输出看[这篇](https://juejin.cn/post/6959043611161952269)

## 5.5 事件代理
把一个元素响应事件（click、keydown......）的函数委托到另一个元素，在冒泡阶段完成。事件委托，会把一个或者一组元素的事件委托到它的父层或者更外层元素上，真正绑定事件的是外层元素，而不是目标元素

## 5.6 setTimeout

```js
var id = setTimeout(func,1000);
clearTimeout(id);
```

返回一个id标识符，在**大约**1000ms后执行func函数（在全局作用域执行）

为什么是大约？JS是单线程，其他代码的运行可能会阻塞该进程

## 5.7 setInterval
每个多少毫秒执行一次。谨慎使用：回调函数进程的阻塞可能导致回调函数堆积

【使用timeout实现interval】


# 6 类

## 6.1 this

### 6.1.1 this对象
this指向函数、类内部对象，运行时自动生成。调用方式决定this对象，谁调用指向谁。

一旦确定，不能被直接更改。

【绑定规则】

- 默认绑定：函数中调用全局变量
- 隐式绑定：作为函数被某个对象调用，绑定到这个对象上
- new绑定：除非函数返回一个对象，否则对函数使用new时将this绑定到赋值对象上
- 显式绑定：使用apply\call\bind改变

new绑定优先级 > 显示绑定优先级 > 隐式绑定优先级 > 默认绑定优先级

### 6.1.2 改变this指向
可以使用`call`, `apply`, `bind`方法

#### 6.1.2.1 call
```js
func.call(obj,1,2);
```

call只生效一次，函数立即执行，传入参数可以不用数组括起来

【手写call】
```js
Function.prototype.myCall = function(context, ...args){
    context = (context === null || context === undefined) ? window : context;
    context.__fn = this;
    let result = context.__fn(...args);
    delete context.__fn;
    return result;
}
```

#### 6.1.2.2 apply

```js
func.apply(obj,[1,2]); // obj是this指向的新对象，传给func的参数必须以数组形式传入
```

apply只生效一次，且是临时生效，函数立即执行，执行完后绑定失效。

如果obj传入null,undefined默认指向浏览器window

【手写apply】
```js
Function.prototype.myApply = function(context,args){
    context = (context === null || context === undefined)? window:context;
    context.__fn = this;
    let result = context.__fn(...args);
    delete context.__fn;
    return result;
}
```

#### 6.1.2.3 bind
```js
let func = oldfunc.bind(obj);
```
bind返回一个绑定永久有效的新函数，参数传递给新函数

```js
Function.prototype.myBind = function(context, ...args1){
    context = (context === null || context === undefined)?window:context;
    let _this = this;
    return function(...args2){
        context.__fn = _this;
        let result = context.__fn(...[...args1,...args2]);
        delete context.__fn;
        return result;
    }
}
```

## 6.2 new

new一个类：
1. 创建一个新对象
2. 将构造函数的作用域赋给新对象（因此this指向了这个新对象）
3. 执行构造函数中的代码（为这个新对象添加属性）
4. 返回新对象

new一个函数：
1. 创建一个新的对象obj
2. 将对象与构建函数通过原型链连接起来
3. 将构建函数中的this绑定到新建的对象obj上
4. 根据构建函数返回类型作判断，如果是原始值则被忽略，如果是返回对象，需要正常处理

【手写new】
```js
function mynew(Func,...args){
    const obj = {};
    obj.__proto__ = Func.prototype;
    let result = Func.apply(obj,args);
    return (typeof result === 'object') ? result : obj;
}
```

## 6.3 原型
原型模式：设计模式，构建一个prototype负责clone新对象

每个对象都拥有一个原型，原型对应的也有自己的原型，一层层向上传递构成原型链

- 一切对象都是继承自Object对象，Object 对象直接继承根源对象null
- 一切的函数对象（包括 Object 对象），都是继承自 Function 对象
- Object 对象直接继承自 Function 对象
- Function对象的__proto__会指向自己的原型对象，最终还是继承自Object对象


## 6.4 继承

- 原型链继承：将子类的prototype设为父类。问题：创建出的子类共享父类属性，修改一个会导致父类修改
- 构造函数继承：使用call将this强行绑定。问题：只能继承父类的实例属性和方法，无法继承prototype方法
- 组合以上两种继承：相当于调用了两次父类，解决以上问题但是导致性能下降
- 原型式继承：使用`Object.create()`，相当于浅拷贝了一份（修改属性会导致原始对象的修改）
- 寄生式继承：封装一个函数，其中仍然使用`Object.create()`创建对象，为这个对象添加一些方法
- 寄生组合式继承

ES6：直接用extends


# 7 优化

## 7.1 节流
阻止一些回调函数的不断触发。

定义：**n 秒内**只运行一次，若在 n 秒内重复触发，只有一次生效

【手写】
```js
function throttle(fn,delay){
    var prev = null;
    return function(){
        var args = arguments;
        var now = Date.now();
        if(now-prev > delay){
            fn.apply(this,args);
            prev = now;
        }
    }
}
```

## 7.2 防抖
定义：**n 秒后**在执行该事件，若在 n 秒内被重复触发，则重新计时

【手写】
```js
function(fn,delay){
    let timer = null;
    return function(){
        let args = arguments;
        clearTimeout(timer);
        timer = setTimeout(() => {
            fn.apply(this,args);
        },delay);
    }
}
```

# 8 ES6 新特性

除了以下罗列的以外，还包括set，map，promise

## 8.1 Generator

## 8.2 Proxy

## 8.3 Module

## 8.4 Decorator

# 9 JS内存机制

## 9.1 引用
每个对象拥有一个关于原型的隐式引用，以及关于属性的显式引用

如果使用引用计数法无法解决循环引用导致的内存泄漏问题

## 9.2 垃圾回收
【引用计数法】

无法解决循环引用的问题。


【标记-清除算法】

从全局根开始，将无法被获取访问到的部分内存清除。

缺点：开销大，容易产生内存碎片。

改进：新生代，老生代，使用标记清除算法后把内存归拢到新生代区域

## 9.3 内存泄露
程序未能释放且不能再被使用的内存

- 意外的全局变量：在函数中使用全局变量或者用this创建全局变量（解决方案：使用严格模式）
    ```js
    function foo(arg) {
        bar = "this is a hidden global variable";
    }

    function foo() {
        this.variable = "potential accidental global";
    }
    // foo 调用自己，this 指向了全局对象（window）
    foo()
    ```
- 定时器：获取到的元素在dom中被删除，但是定时器仍然存在，定时器拥有的资源不会被释放
    ```js
    var someResource = getData();
    setInterval(function() {
        var node = document.getElementById('Node');
        if(node) {
            // 处理 node 和 someResource
            node.innerHTML = JSON.stringify(someResource);// someResource不会被释放
        }
    }, 1000);
    ```
- 闭包：闭包内使用的引用导致不会释放
    ```js
    function bindEvent() {
        var obj = document.createElement('XXX');
        var unused = function () {
            console.log(obj, '闭包内引用obj obj不会被释放');
        };
        obj = null; // 解决方法
    }
    ```
- 没有清理对dom元素的引用：dom元素在被删除后还存在对其的引用
    ```js
    const refA = document.getElementById('refA');
    document.body.removeChild(refA); // dom删除了
    console.log(refA, 'refA'); // 但是还存在引用能console出整个div 没有被回收
    refA = null; // 解决办法
    console.log(refA, 'refA'); // 解除引用
    ```

## 9.4 存储方式

### 9.4.1 cookie
保持登陆状态 => http无状态

cookie在每次请求中都会被发送

每个域名下Cookie的数量不能超过20个，每个Cookie的大小不能超过4kb

【cookie安全】

带有secure属性只能被https协议发送。如果带有httponly属性不能被js操纵，只能是服务端cookie

【过期时间】

不设置默认为会话周期，即浏览器关闭后cookie失效

max-age以秒为单位，区别于http的max-age，http以正负表示

【总结-cookie字段】


### 9.4.2 localStorage

不会过期，每个域5MB

【存满了之后？】
- 报错 try-catch
- 使用其他域的存储空间
- 使用一些淘汰机制？

### 9.4.3 sessionStorage
当前会话结束后即被清除，每个域5MB

【跨标签页同源sessionStorage访问】

使用localStorage？

### 9.4.4 变量堆栈存储

- 局部变量存储在栈中，如果是对象，栈中存储对象的引用
- 全局变量和被捕获变量都存在堆中

总结：除了局部变量，其他的都存储在堆中。

# 10 严格模式

## 10.1 设置严格模式的目的
- 消除Javascript语法的一些不合理、不严谨之处，减少一些怪异行为;
- 消除代码运行的一些不安全之处，保证代码运行的安全；
- 提高编译器效率，增加运行速度；
- 为未来新版本的Javascript做好铺垫。

## 10.2 使用方式

```js
"use strict";
```

# 11 DOM

## 11.1 window
高度：innerheight, outerheight

https://zhuanlan.zhihu.com/p/141845423

## 11.2 图片懒加载

### 11.2.1 手动获取图片是否显示

### 11.2.2 IntersectObservable



# Q & A

1. let/const/var区别
    见1.1节
2. js有哪些数据类型
    见1.2节
3. 数据类型判断
    - 1.2.1节typeof


## Frame

面试时经常喜欢提问对比性问题，比如列表元素，在vue中不加key的反应和react中不加key的反应，涉及到框架底层的渲染机制

# Vue

## 渲染流程
1. 解析模板
2. 生成渲染函数
3. 执行渲染函数
4. 对比新旧虚拟dom树：根据diff算法决定需要更新的内容
5. 更新dom

## 生命周期hooks

### 常规hooks

### 父子组件渲染顺序

### keep-alive
在**组件切换**过程中，将组件的状态保存在内存中，防止重复渲染dom。

组件就没有beforeDestroyed和destroyed的生命周期钩子函数，会被替换成activated,beforeactivate

## 双向绑定

MVVM原理

数据劫持（object.defineProperty）+ 发布-订阅模式

### 手写发布-订阅模式

### 数据劫持

使用object.defineProperty的缺点：通过下标方式修改数组数据或者给对象新增属性，这都不能触发组件的重新渲染。

vue2解决方案：重写函数；vue3解决方案：使用proxy监听

### MVVM，MVC，MVP

**MVVM**：model，view，viewmodel，双向绑定，通过viewmodel进行model和view的更新

**MVC**：model，view， controller。view的交互触发controller调用，修改model，触发view更新【观察者模式】

**MVP**：model，view，presenter。解耦view和model，在 Presenter 中将 Model 的变化和 View 的变化绑定在一起，以此来实现 View 和 Model 的同步更新

### watch
支持异步和开销比较大

### computed
缓存，不支持异步；更多的是观察作用触发回调函数

### methods
每次数据更新都会触发method执行

## 语法糖

### 指令系统

#### v-if、v-show
v-if通过操作dom树，v-show改变css的display属性值

#### v-if、v-for优先级

### slot
获取传进`<></>`之间的值

## axios


## 单屏

## 组件通信方式

## 虚拟dom

### diff算法

### key


### vue3优化
增加一些静态标记，对静态节点不进行重复的渲染

## Vue3和Vue2

Vue3的优化：
- 更小：移除一些不常用api
- 更快：编译速度更快
- 支持ts
- 使用proxy替代defineProperty进行数据劫持
- tree shaking: 只有需要的包才会被打包使用



## Vuex

# React

## hooks

### state和props

### useState useEffect useCallback useMemo

## 函数式组件和类式组件

## 虚拟dom

## 组件通信

## diff算法

## 生命周期


# Vue VS React

React特点总结：
- JSX：使用javascript写html
- functional programming
- lifecycle hooks
- react native for mobile devices

Vue特性：
- html、js、css集成在一个文件中
- syntatic sugar: v-if v-for
- slot

【相同点】
- 都有组件化思想
- 都支持服务器端渲染
- 都有Virtual DOM（虚拟dom）
- 数据驱动视图
- 都有支持native的方案：Vue的weex、React的React native
- 都有自己的构建工具：Vue的vue-cli、React的Create React App
【区别】
- 数据流向的不同。react从诞生开始就推崇单向数据流，而Vue是双向数据流
- 数据变化的实现原理不同。react使用的是不可变数据，而Vue使用的是可变的数据
- 组件化通信的不同。react中我们通过使用回调函数来进行通信的，而Vue中子组件向父组件传递消息有两种方式：事件和回调函数
- diff算法不同。react主要使用diff队列保存需要更新哪些DOM，得到patch树，再统一操作批量更新DOM。Vue 使用双向指针，边对比，边更新DOM

# 前端性能优化

## 优化思路
浏览器 -> 资源加载（图片） -> 代码

## 评价指标

- 白屏时间
- 页面渲染时间
- 最大内容加载时间

## 优化白屏

- DNS服务优化
- CDN内容分发网络
- 服务端优化（缓存与分包）

## 优化渲染

- JS：使用防抖优化用户输入
- CSS样式：减少复杂的样式计算和嵌套；避免大的、复杂的布局和布局回流；异步加载非必须css

## 最大内容加载


