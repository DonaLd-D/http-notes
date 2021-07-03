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
