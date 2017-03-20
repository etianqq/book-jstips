#Ajax

Ajax，可以通过延迟下载体积较大的资源文件来使的页面加载速度更快（不会阻塞window.onload事件）。

####数据传输

数据传输首推XMLHttpRequest(XHR)，它允许异步发送和接受数据。

有一种新技术叫做MultiPart XHR，其允许客户端只用一个HTTP请求就可以从服务端取得多个资源。
关键点：
* 服务端将资源（CSS文件，HTML片段，JS代码，base64编码的图片）打包成一个由双方约定好的字符串分割的长字符串并发送到客户端
* JS代码处理这个长字符串

处理代码为：
```
function handleImageData(data, mimeType) { 
 var img = document.createElement('img'); 
 img.src = 'data:' + mimeType + ';base64,' + data; 
 return img; 
} 
function handleCss(data) { 
 var style = document.createElement('style'); 
 style.type = 'text/css'; 
 var node = document.createTextNode(data); 
 style.appendChild(node); 
 document.getElementsByTagName_r('head')[0].appendChild(style); 
} 
function handleJavaScript(data) { 
 eval(data); 
}
```
