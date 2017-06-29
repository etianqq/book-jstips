#HTTP 编解码

用户从浏览器端发起一个HTTP请求，需要存在编码的地方是URL，Cookie，Parameter，服务器端接受到HTTP请求后要解析HTTP，将URL，Cookie，Parameter解码。流程如下图：

![](/assets/http encoding.png)

####1. URL编解码

浏览器 