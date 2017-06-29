#HTTP 编解码

用户从浏览器端发起一个HTTP请求，需要存在编码的地方是URL，Cookie，Parameter，服务器端接受到HTTP请求后要解析HTTP，将URL，Cookie，Parameter解码。流程如下图：

![](/assets/http encoding.png)

####1. HTTP请求过程中的编解码

浏览器编码URL是将非ASCII字符按照某种编码格式编码成16进制数字，并在每个16进制数字前面加上%符号。

GET请求的参数都是附加在URL上面，所以GET请求参数遵循URL编码，使用浏览器默认编码格式编码。

POST请求参数通过HTTP的Body传递到服务端，根据Content-Type的charset编码格式对提交参数编码。

用户请求的资源获得成功后，内容通过response返回到客户端浏览器，内容根据Content-Type的charset编码格式进行解码。如果Content-Type没有设置charset，那么，浏览器根据HTML的```<meta charset="UTF-8">```解码。如果这个也没有定义，那么浏览器将使用默认编码来解码。

####2. JS中的编码问题

外部引入JS文件，如果JS文件设置charset，浏览器就会以此解析这个JS文件，否则以当前HTML页面编码格式解码。

注意：如果JS文件与当前页面的编码格式不一致，那么，JS文件中的中文字符就变成乱码。

#####JS的URL编码

JS中，处理URL编码的函数有三个```escape```，```encodeURI```和```encodeURIComponent```。

