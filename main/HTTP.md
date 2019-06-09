# HTTP

## 概念
基于TCP协议，属于OSI应用层的面向对象的超文本传输协议。

## http, http1.1, http2, https
### request
#### 状态行
- request method
    - get, post, head, put, delete, connect, options, trace
- request URI
- request version
    - HTTP/1.0
    - HTTP/1.1
        - 默认keep-alive, 减少握手开销; 可只发header, 节约带宽; 支持host域参数
    - HTTP/2.0
        - 多路复用(多重请求)(二进制分帧)、流优先级、服务器推送、头部压缩、应用层协商协议
    - HTTPS
        - ssl原理, CA证书, 签名, 公钥, 私钥, 对称秘钥...
#### 状态头
- Accept-Encoding
- Authorization
- Cookie
- Content-Length
- Content-Type
- User-Agent
#### 状态体

### response
#### 响应行
##### response version
- HTTP/1.0
- HTTP/1.1
- HTTP/2.0
- HTTPS
##### status code
- 100   (继续) 请求者应当继续提出请求。 服务器返回此代码表示已收到请求的第一部分,正在等待其余部分。    
- 101   (切换协议) 请求者已要求服务器切换协议,服务器已确认并准备切换。
- 200   (成功)  服务器已成功处理了请求。 通常,这表示服务器提供了请求的网页。   
- 201   (已创建)  请求成功并且服务器创建了新的资源。   
- 202   (已接受)  服务器已接受请求,但尚未处理。   
- 203   (非授权信息)  服务器已成功处理了请求,但返回的信息可能来自另一来源。   
- 204   (无内容)  服务器成功处理了请求,但没有返回任何内容。   
- 205   (重置内容) 服务器成功处理了请求,但没有返回任何内容。  
- 206   (部分内容)  服务器成功处理了部分 GET 请求。   
- 300   (多种选择)  针对请求,服务器可执行多种操作。 服务器可根据请求者 (user agent) 选择一项操作,或提供操作列表供请求者选择。   
- 301   (永久移动)  请求的网页已永久移动到新位置。 服务器返回此响应(对 GET 或 HEAD 请求的响应)时,会自动将请求者转到新位置。  
- 302   (临时移动)  服务器目前从不同位置的网页响应请求,但请求者应继续使用原有位置来进行以后的请求。  
- 303   (查看其他位置) 请求者应当对不同的位置使用单独的 GET 请求来检索响应时,服务器返回此代码。  
- 304   (未修改) 自从上次请求后,请求的网页未修改过。 服务器返回此响应时,不会返回网页内容。   
- 305   (使用代理) 请求者只能使用代理访问请求的网页。 如果服务器返回此响应,还表示请求者应使用代理。   
- 307   (临时重定向)  服务器目前从不同位置的网页响应请求,但请求者应继续使用原有位置来进行以后的请求。
- 400   (错误请求) 服务器不理解请求的语法。   
- 401   (未授权) 请求要求身份验证。 对于需要登录的网页,服务器可能返回此响应。   
- 403   (禁止) 服务器拒绝请求。  
- 404   (未找到) 服务器找不到请求的网页。  
- 405   (方法禁用) 禁用请求中指定的方法。   
- 406   (不接受) 无法使用请求的内容特性响应请求的网页。   
- 407   (需要代理授权) 此状态代码与 401(未授权)类似,但指定请求者应当授权使用代理。  
- 408   (请求超时)  服务器等候请求时发生超时。   
- 409   (冲突)  服务器在完成请求时发生冲突。 服务器必须在响应中包含有关冲突的信息。   
- 410   (已删除)  如果请求的资源已永久删除,服务器就会返回此响应。   
- 411   (需要有效长度) 服务器不接受不含有效内容长度标头字段的请求。   
- 412   (未满足前提条件) 服务器未满足请求者在请求中设置的其中一个前提条件。   
- 413   (请求实体过大) 服务器无法处理请求,因为请求实体过大,超出服务器的处理能力。   
- 414   (请求的 URI 过长) 请求的 URI(通常为网址)过长,服务器无法处理。   
- 415   (不支持的媒体类型) 请求的格式不受请求页面的支持。   
- 416   (请求范围不符合要求) 如果页面无法提供请求的范围,则服务器会返回此状态代码。   
- 417   (未满足期望值) 服务器未满足"期望"请求标头字段的要求。   
- 500   (服务器内部错误)  服务器遇到错误,无法完成请求。   
- 501   (尚未实施) 服务器不具备完成请求的功能。 例如,服务器无法识别请求方法时可能会返回此代码。   
- 502   (错误网关) 服务器作为网关或代理,从上游服务器收到无效响应。   
- 503   (服务不可用) 服务器目前无法使用(由于超载或停机维护)。 通常,这只是暂时状态。   
- 504   (网关超时)  服务器作为网关或代理,但是没有及时从上游服务器收到请求。   
- 505   (HTTP 版本不受支持) 服务器不支持请求中所用的 HTTP 协议版本。  
#### 响应头
Content-Encoding  
Content-Length  
Expires  
Set-Cookie  

#### 响应体  

### 通讯流程
#### 三次握手
流程
- C->S: syn seq=j // 在吗
- S->C: ack j+1, syn seq=k // ok, 在
    - S: syn_recv
- C->S: ack k+1 // ok, 建立连接吧
    - C: syn_send
    - C: established
    - S: established
意义: 当第一次握手出现网络延迟， 第二次握手依然会正常响应， 这时第三次握手就会被抛弃，服务端没收到第三次握手就不会建立连接。反之，若无第三次握手，服务端在第二次握手就开始建立客户端已经认为过期抛弃的连接， 浪费资源。

#### 四次挥手
流程:
- C->S: fin seq=i // 我要关了
- S->C: ack i+1 // ok, 等下, 我还没发完呢
    - S: close_wait
    - C: fin_wait1
- S->C: fin seq=j // (发完了)我关了, 你也关吧
    - S: last_wait
    - C: fin_wait2
- C->S: ack j+1 // ok, 我也关了, 并且轮询几下检测是否真断了。
    - C: time_wait
    - C: closed
    - S: closed
意义: 第二，三次挥手的意义在于，服务端可能不会立即关闭socket，故只能先回复一个ack确认。
意义: 第四次挥手会进入time_wait状态， 重发几次以确认服务端是否已经断开。
