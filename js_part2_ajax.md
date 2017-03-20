#Ajax

Ajax，可以通过延迟下载体积较大的资源文件来使的页面加载速度更快（不会阻塞window.onload事件）。

数据传输首推XMLHttpRequest(XHR)，它允许异步发送和接受数据。

####MultiPart XHR

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

缺点：
资源不能被浏览器缓存。

####JSONP
JSONP并没有使用XHR对象，它利用script标签发起请求。

* 优点：支持跨域请求数据
* 缺点：只能是GET请求；不能设置请求超时处理/请求失败

```
使用XHR时，GET请求比POST更快（少量数据）。
一个GET请求只发送一个数据包到服务器。
一个POST请求至少发送两个数据包，一个装载头信息，另一个装载POST正文。
```

####信标（beacons）
类似动态脚本注入。
使用场景：
* 不需要服务端返回数据（服务端可以返回204 No Content）
* 只能是GET请求

代码：
```
var url = '/status_tracker.php'; 
var params = [ 
 'step=2', 
 'time=1248027314' 
]; 
var beacon = new Image(); 
beacon.src = url + '?' + params.join('&'); 
beacon.onload = function() { 
 if (this.width == 1) { 
   // Success. 
 } 
 else if (this.width == 2) { 
   // Failure; create another beacon and try again. 
 } 
}; 
beacon.onerror = function() { 
   // Error; wait a bit, then create another beacon and try again. 
};
```

####加速AJAX

* 减少请求数，如使用MXHR
* 缩短页面加载时间，页面主要内容加载完成后，用Ajax获取次要文件
* 确保错误代码不会输出给用户，并在服务端处理错误