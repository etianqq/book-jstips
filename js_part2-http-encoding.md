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

######1. escape

将ASCII码字母，数字，标点符号``` - _ . ! ~ * ' ( )```之外的其它字符转化成**Uicode**编码值，并在编码值前加上```%u```。

```
escape("i am 邱");
输出：i%20am%20%u90B1
```
注意：escape()和unescape()已经从ECMAScript v3标准中删除了，URL的编码可以用```encodeURI```和```encodeURIComponent```来替代。
######2. encodeURI

encodeURI()是真正的JS用来对URL编码的函数，它可以将整个URL进行**UTF-8**编码。
注意：下面字符不会编码
* 不会对 ASCII 字母和数字进行编码
* 不会对ASCII 标点符号进行编码： ```- _ . ! ~ * ' ( )```
* 不会对 URI 中具有特殊含义的 ASCII 标点符号进行编码：```;/?:@&=+$,#```

```
encodeURI("http://etianqq.duapp.com?name=邱")
输出：http://etianqq.duapp.com?name=%E9%82%B1
```
######3. encodeURIComponent

除了下面字符，encodeURIComponent会对所有字符编码。
* 不会对 ASCII 字母和数字进行编码
* 不会对ASCII 标点符号进行编码： ```- _ . ! ~ * ' ( )```

此函数通常用于将一个URL放在另一个URL参数中。


