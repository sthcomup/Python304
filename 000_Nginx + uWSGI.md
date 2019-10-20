- uWSGI的理解

  >1.uWSGI 是一个 Web 服务器，它实现了 WSGI 协议、uwsgi、http 等协议。Nginx 中HttpUwsgiModule 的作用是与 uWSGI 服务器进行交换。WSGI 是一种 Web 服务器网关接口。它是一 个 Web 服务器(如 nginx，uWSGI 等服务器)与 web 应用(如用 Flask 框架写的程序)通信的一种 规范。

- WSGI / uwsgi / uWSGI 这三个概念的区分

  >WSGI 是一种通信协议。
  >uwsgi 是一种线路协议而不是通信协议，在此常用于在 uWSGI 服务器与其他网络服务器的数据通信。
  >
  >uWSGI 是实现了 uwsgi 和 WSGI 两种协议的 Web 服务器。

- Nginx的理解
  - nginx 是一个开源的高性能的 HTTP 服务器和反向代理
  - 作为 web 服务器，它处理静态文件和索引文件效果非常高
  - 它的设计非常注重效率，最大支持 5 万个并发连接，但只占用很少的内存空间
  - 稳定性高，配置简洁
  - 强大的反向代理和负载均衡功能，平衡集群中各个服务器的负载压力应用

- nginx 和 uWISG 服务器之间如何配合工作

  >首先浏览器发起 http 请求到 nginx 服务器，Nginx 根据接收到请求包，进行 url 分析，判断访问的 资源类型，如果是静态资源，直接读取静态资源返回给浏览器，如果请求的是动态资源就转交给 uwsgi服务器，uwsgi 服务器根据自身的 uwsgi 和 WSGI 协议，找到对应的 Django 框架，Django 框架下的 应用进行逻辑处理后，将返回值发送到 uwsgi 服务器，然后 uwsgi 服务器再返回给 nginx，最后 nginx将返回值返回给浏览器进行渲染显示给用户。
  >
  >

- nginx负载均衡保持session会话一致

  >负载均衡时，为了保证同一用户session会被分配到同一台服务器上，可以使用以下方法：
  >
  >1.使用cookie将用户的session存入cookie里，当用户分配到不同的服务器时，先判断服务器是否存在该用户的session，如果没有就先把cookie里面的sessoin存入该服务器，实现session会话保持。缺点是存入cookie有安全隐患。
  >
  >2.使用缓存利用memcache，Redis等缓存分布式的特点，可以将所有服务器产生的session存入同一台服务器的缓存中，实现session共享。这样安全性比较高，而且从内存中读取session比从文件中读取速度快。
  >
  >3.使用ip_hash如果是nginx服务器的负载均衡，可以在upstream里设置ip_hash，每个请求按访问ip的hash结果分配，映射到固定某一台的服务器。缺点是可能导致负载不均衡，不适合单点登录。