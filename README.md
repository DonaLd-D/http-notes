### 互联网协议
- 物理层（双绞线、光纤、无线电波）
- 数据链路层（通过ARP协议来获取接受方的MAC地址（网卡））
- 网络层（IP协议）
- 传输层（”端口”（port），每一个使用网卡的程序的编号）
- 会话层（概念，tcp连接等）
- 表示层（Recognizing data,HTML,DOC,JPEG,MP3,AVL Sockets,负责数据解包）
- 应用层（DNS,WWW/HTTP,P2P,EMAIL/POP,SMTP,Telnet,ftp，解决业务问题）

### 浏览器输入url后发生了什么？
- 1.DNS域名解析
  - comDNS服务器，orgDNS服务器，netDNS服务器
  - 客户端收到输入的域名地址后，它首先去找本地的hosts文件，检查在该文件中是否有相应的域名、IP对应关系
  - 如果有，则向其IP地址发送请求，如果没有，再去找DNS服务器。
- 2.建立TCP连接
  - 三次握手
  - 互相确认自己是否发送正常和接收正常
- 3.发送HTTP请求
  - 请求首部字段
  - 通用首部字段
  - 实体首部字段
- 4.服务器处理请求
  - Apache、Ngnix、IIS等
- 5.返回响应结果
  - 响应首部字段
  - 通用首部字段
  - 实体首部字段
- 6.关闭TCP连接
  - 四次挥手
  - 互相确认并断开连接
- 7.浏览器解析HTML
  - 浏览器通过解析HTML，生成DOM树，
  - 解析CSS，生成CSS规则树，
  - 然后通过DOM树和CSS规则树生成渲染树。
  - 渲染树与DOM树不同，渲染树中并没有head、display为none等不必显示的节点。
- 8.浏览器布局渲染
  - replaint：屏幕的一部分重画，不影响整体布局，比如某个CSS的背景色变了，但元素的几何尺寸和位置不变。
  - reflow： 意味着元件的几何尺寸变了，我们需要重新验证并计算渲染树。是渲染树的一部分或全部发生了变化。这就是Reflow，或是Layout。

### TCP 三次握手和四次挥手
- 三次握手（建立连接）
  - 第一次握手（客户端发送 SYN 报文给服务器，服务器接收该报文）：客户端什么都不能确认；服务器确认了对方发送正常，自己接收正常
  - 第二次握手（服务器响应 SYN 报文给客户端，客户端接收该报文）：客户端确认了：自己发送、接收正常，对方发送、接收正常；服务器确认了：对方发送正常，自己接收正常
  - 第三次握手（客户端发送 ACK 报文给服务器）：客户端确认了：自己发送、接收正常，对方发送、接收正常； 服务器确认了：自己发送、接收正常，对方发送、接收正常
- 四次挥手（断开连接）
  - 第一次挥手：客户端发送一个 FIN 报文（请求连接终止：FIN = 1），报文中会指定一个序列号 seq = u。并停止再发送数据，主动关闭 TCP 连接。此时客户端处于 FIN_WAIT1 状态，等待服务端的确认。
  - 第二次挥手：服务端收到 FIN 之后，会发送 ACK 报文，且把客户端的序号值 +1 作为 ACK 报文的序列号值，表明已经收到客户端的报文了，此时服务端处于 CLOSE_WAIT状态。
  - 第三次挥手：如果服务端也想断开连接了（没有要向客户端发出的数据），和客户端的第一次挥手一样，发送 FIN 报文，且指定一个序列号。此时服务端处于 LAST_ACK 的状态，等待客户端的确认。
  - 第四次挥手：客户端收到 FIN 之后，一样发送一个 ACK 报文作为应答（ack = w+1），且把服务端的序列值 +1 作为自己 ACK 报文的序号值（seq=u+1），此时客户端处于 TIME_WAIT（时间等待）状态。

### HTTP/0.9(传输超文本)
- 1991 年 HTTP（HyperText Transfer Protocol，超文本传输协议）正式诞生，当时的版本是 0.9。从名字可以看出，该协议的作用是传输传输超文本内容 HTML。
- 协议定义了客户端发起请求、服务端响应请求的通信模式。请求报文内容只有 1 行

### HTTP/1.0（传输脚本、样式、图片、音频和视频等不同类型的文件）
- 增加了 HEAD、POST 等新方法
- 增加了响应状态码，标记可能的错误原因
- 引入了协议版本号概念
- 引入了 HTTP Header（头部）的概念，让 HTTP 处理请求和响应更加灵活
- 传输的数据不再局限于文本
- HTTP/1.0 并不是一个“标准”，只是一份参考文档，不具有实际的约束力。

### HTTP/1.1（解决传输问题，引入长连接，并发连接，管道机制）
- `可以开启多个 TCP 连接，任何一个 TCP 出现问题都不会影响其他 TCP 连接，剩余的 TCP 连接还可以正常传输数据`
- `浏览器为了减轻服务器的压力，限制了同一个域名下的 HTTP 连接数，即 6 ~ 8 个`
- 长连接：引入了 TCP 连接复用，即一个 TCP 默认不关闭，可以被多个请求复用
- 并发连接：对一个域名的请求允许分配多个长连接（缓解了长连接中的「队头阻塞」问题）
- 引入管道机制，一个 TCP 连接，可以同时发送多个请求。（响应的顺序必须和请求的顺序一致，因此不常用）
- 增加了 PUT、DELETE、OPTIONS、PATCH 等新的方法
- 新增了一些缓存的字段（If-Modified-Since, If-None-Match）
- 请求头中引入了 range 字段，支持断点续传
- 允许响应数据分块（chunked），利于传输大文件
- 强制要求 Host 头，让互联网主机托管称为可能

### HTTP/2（解决连接问题，改为二进制数据提升传输效率，利用一个连接来发送多个请求，即多路复用）
- `HTTP/2.0 虽然已经发布了 6 年，不过由于 HTTP/1.1 实在太过经典和强势，目前 HTTP/2.0 的普及率还比较低，仍然有很多网站使用的是 HTTP/1.1 版本。`
- `通常只使用一个 TCP 连接进行传输，在丢包或网络中断的情况下后面的所有数据都被阻塞`
- 数据通过二进制协议传输，不再是纯文本
- 多路复用，废弃了 1.1 中的管道
- 使用专用算法压缩头部，减少数据传输量
- 通过设置数据帧的优先级，让服务器优先处理某些请求
- 允许服务器主动向客户推送数据
- 头部字段全部改为小写；引入了伪头部的概念，出现在头部字段之前，以冒号开头
- 增强了安全性，“事实上”要求加密通信

### HTTP/3
- 2018 年 HTTP/3 将底层依赖的 TCP 改成 UDP

### HTTP请求方法
* 根据HTTP标准，HTTP请求可以使用多种请求方法。
* HTTP1.0定义了三种请求方法：GET,POST和HEAD方法。
* HTTP1.1新增了六种请求方法：OPTIONS,PUT,PATCH,DELETE,TRACE和CONNECT方法。
> - __get__ 请求指定的页面信息，并返回实体主体。
> - __head__ 类似get请求，只不过返回的响应中没有具体的内容，用于获取报头
> - __post__ 向指定资源提交数据进行处理请求。数据被包含在请求体中。post请求可能会导致新的资源的建立和/或已有资源的修改。
> - __put__ 从客户端向服务器传送的数据取代指定的文档的内容。
> - __delete__ 请求服务器删除指定的页面。
> - __connect__ http/1.1协议中预留给能够将连接改为管道方式的代理服务器。
> - __options__ 允许客户端查看服务器的性能。
> - __trace__ 会显服务器收到的请求，主要用于测试或诊断。
> - __patch__ 是对put方法的补充，用于对已知资源进行局部更新。

***

### HTTP状态码
##### 常见的http状态码：
> - **200** 请求成功
> - **301** 资源（网页等）被永久转移到其他URL
> - **404** 请求的资源（网页等）不存在
> - **500** 内部服务器错误
##### http状态码分类
> - **1xx** 信息，服务器收到请求，需要请求着继续执行操作
> - **2xx** 成功，操作被成功接收并处理
> - **3xx** 重定向，需要进一步的操作以完成请求
> - **4xx** 客户端错误，请求包含语法错误或无法完成请求
> - **5xx** 服务器错误，服务器在处理请求的过程中发生了错误

### HTTP content-type
content-type标头告诉客户端实际返回的内容的内容类型。
##### 常见的媒体格式类型如下：
> - **text/html** html格式
> - **text/plain** 纯文本格式
> - **text/xml** xml格式
> - **image/gif** gif格式
> - **image/jpeg** jpg格式
> - **image/png** png格式
##### 以application开头的媒体格式类型：
> - **application/xhtml+xml** xhtml格式
> - **application/xml** xml数据格式
> - **application/atom+xml** atom xml聚合格式
> - **application/json** json数据格式
> - **application/pdf** pdf格式
> - **application/msword** word文档格式
> - **application/octet-stream** 二进制流数据（如常见的文件下载）
> - **application/x-www-form-urlencoded**  `<from encType=">`中默认的encType,form表单数据被编码为key/value格式发送到服务器（表单默认的提交数据的格式）
##### 另外一种常见的媒体格式是上传文件之时使用的：
> - **multipart/form-data** 需要在表单中进行文件上传时，就需要使用该格式
  
***

### HTTP中的请求头和响应头属性

#### 一次完整的HTTP请求所经历的7个步骤
  1. 建立TCP连接
  2. Web浏览器向web服务器发送请求命令  例如：GET /sample/hello.jsp HTTP 1.1
  3. Web浏览器发送请求头信息
  4. Web服务器应答  例如：HTTP/1.1 200 ok
  5. Web服务器发送应答头信息
  6. Web服务器向浏览器发送数据
  7. Web服务器关闭TCP连接

#### General  Headers 通用信息头
  1.  Request  URL      请求的地址
  2.  Request  Method    请求的方法类型
  3.  Status  Code      响应状态码
  4.  Remote  Address    表示远程服务器地址       
  5.  Referrer Policy 

#### Response Headers   响应头
  1.  Content-Length   响应体的长度
  2.  Content-type     返回的响应MIME类型与编码:告诉浏览器它发送的数据属于什么文件类型   
  3.  Cache-control    指定请求和响应遵循的缓存机制
    1）public 响应可被任何缓存区缓存
    2）private 对于单个用户的整个或部分响应消息，不能被共享缓存处理
    3）no-cache 表示请求或响应消息不能缓存
  4.  date         原始服务器消息发出的时间
  5.  Server        web服务器软件名称
  6.  Last-Modified   标记请求的资源在服务器端最后被修改的时间

#### Request  Headers  请求头
  1. Accept        告诉服务器可以接受的文件格式。根据Accept头的不同，按照相应的顺序进行produces的匹配。
  2. Accept-Encoding  gzip,deflate,sdch,br 指定浏览器可以支持的web服务器返回的内容压缩编码类型
  3. Accept-Language  浏览器支持的语言
  4. Cache-Control   指定请求和响应遵循的缓存机制
  5. Connection     keep-alive 表示是否需要持久连接
  6. Cookie        HTTP请求发送时，会把保存在该请求域名下的所有cookie值一起发送给web服务器
  7. Host         指定请求的服务器的域名和端口号
  8. Referer       告诉服务器是从哪个网站链接过来的，提供访问来源的信息
  9. User-Agent     用户代理：简称UA。内容包含发出请求的用户信息，使得服务器能够识别客户端使用的操作系统及版本、CPU类型、浏览器及版本、浏览器渲染引擎、浏览器语言、插件等。
  10. Authorization   当客户端访问受口令保护时，服务器端会发送401状态码和www-authenticate 响应头，要求客户端使用Authorization来应答

### get和post的区别
- GET后退按钮/刷新无害，POST数据会被重新提交（浏览器应该告知用户数据会被重新提交）。
- `GET书签可收藏，POST为书签不可收藏。`
- `GET能被缓存，POST不能缓存 。`
- GET编码类型application/x-www-form-url，POST编码类型encodedapplication/x-www-form-urlencoded 或 multipart/form-data。为二进制数据使用多重编码。
- GET历史参数保留在浏览器历史中。POST参数不会保存在浏览器历史中。
- GET对数据长度有限制，当发送数据时，GET 方法向 URL 添加数据；URL 的长度是受限制的（URL 的最大长度是 2048 个字符）。POST无限制。
- GET只允许 ASCII 字符。POST没有限制。也允许二进制数据。
- 与 POST 相比，GET 的安全性较差，因为所发送的数据是 URL 的一部分。在发送密码或其他敏感信息时绝不要使用 GET ！POST 比 GET 更安全，因为参数不会被保存在浏览器历史或 web 服务器日志中。
- GET的数据在 URL 中对所有人都是可见的。POST的数据不会显示在 URL 中。


