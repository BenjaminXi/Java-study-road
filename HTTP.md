# <a id="HTTP">HTTP</a>

#### <a id="cookie">Cookie是什么？Cookie的作用？</a>
* Cookie：当前识别用户，实现持久会话的最好方式。Cookie可以笼统地分为两类：会话cookie和持久cookie。前者为临时cookie，记录了用户访问站点时的设置和偏好，用户退出浏览器时，会话cookie就删除了。持久cookie的生存时间更长一些，存储在硬盘上，浏览器退出，计算机重启时仍然存在。通常会用持久cookie维护某个用户周期性访问的站点的站点的配置文件或登录名。这两者的唯一区别是它们的过期时间。
* Cookie的作用：当用户首次访问web服务器时，web服务器对用户一无所知。Web服务器会希望用户再次访问，所以给用户拍上一个独有的cookie，这样以后就可以识别出用户了。Cookie中包含了由name=value这样的信息列表，通过set-cookie HTTP响应首部将其贴到用户身上。Cookie通常包含一个服务器为了进行跟踪而产生的识别码。浏览器会记住从服务器返回的set-cookie首部中cookie内容，并将cookie集存储在浏览器的cookie数据库中，将来用户返回同一站点时，浏览器会挑中那个服务器贴到用户身上的那些cookie，并在一个cookie请求首部中将其传回去。

#### <a id ="HTTP请求">HTTP请求的全过程。</a>
1. 浏览器从URL中解析出服务器的主机名；
2. 浏览器从将主机名转换为IP地址；
3. 浏览器将端口号从URL中解析出来；
4. 浏览器建立一条与web服务器的TCP连接；
5. 浏览器向服务器发送一条HTTP请求报文；
6. 服务器向浏览器回送一条HTTP响应报文；
7. 关闭连接，浏览器显示文档。

#### <a id ="HTTP请求头信息">HTTP请求头信息。</a>
HTTP报文包含三部分：起始行，头部和主体。HTTP报文分为两类：请求报文和响应报文。起始行包含方法、状态码、原因短语和版本号。首部向请求和响应报文添加了一些附加信息，本质上，是一些名/值对的列表。首部可以分为以下几类：通用首部、请求首部、响应首部、实体首部和扩展首部。

请求首部用于说明谁在发送请求、请求来自何处、或者客户端的喜好及能力，浏览器根据请求首部，为客户端提供更好的响应。
* 信息性首部中有client-IP、From、Host、Refer、UA-Color、UA-CPU、UA-DISP、UA-OS、UA-Pixels、User-Agent。
* Accept首部为客户端提供了将其喜好和能力告知服务器的方式，包括Accept、Accept-Charset、Accept-Encoding、Accept-Language、TE。
* 条件请求首部为请求加上了限制，包括：Except、If-Match、If-Modified-Since、If-None-Match、If-Range、If-Unmodified-Since、Range。
* 安全请求首部对请求进行质询/响应认证，包括：Authorization、Cookie、Cookie2。
* 代理请求首部包括：Max-Forward、Proxy-Authorization、Proxy-Connection。


#### <a id ="get,post,delete,put,option的作用">get,post,delete,put,option的作用</a>
get：用于请求服务器返回某个资源</br>
post：向服务器输入数据</br>
put：向服务器写入文档</br>
options：请求服务器告知其支持的各种功能</br>
delete：请求服务器删除指定URL的资源</br>

#### <a id ="get和post的区别">get和post的区别</a>

* 请求参数：get的请求参数在URL之后，长度有限；post请求参数位置在消息体中，适合安全传输，可以上传大量数据；
* 缓存：get可避免缓存，浏览器从缓存中读取；
* 标签：get方便用户设定标签，post请求参数不在地址栏，无法加入书签；
* 等幂：get为等幂操作（同一操作重复多次，返回同样的结果），post为非等幂操作；

#### <a id ="cookie&sessionStorage&localStorage的区别">cookie,sessionStorage,localStorage的区别</a>

* 生命周期：cookie由服务器设置失效时间，过期之后cookie和cookie数据被删除；sessionStorage关闭页面后被清除；localStorage会永久储存，除非被删除；
* 存放数据大小：cookie一般为4K左右；sessionStorage和localStorage一般为5MB；
* 作用域：cookie在所有同源窗口中都是共享的；sessionStorage在不同的浏览器窗口中不共享，即使是同一个页面；localStorage 在所有同源窗口中都是共享的；
* 位置：cookie数据始终在同源的http请求中携带（即使不需要），即cookie在浏览器和服务器间来回传递。而sessionStorage和localStorage不会自动把数据发给服务器，仅在本地保存。
