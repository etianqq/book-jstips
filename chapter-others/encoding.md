# 前端的各种转义


在使用 **外部数据** 时，以下场景下我们要考虑转义：

+ 作为 HTML 的一部分
+ 作为 JS 的一部分
+ 作为 innerHTML
+ 作为 url 或 url 的组件
+ 作为表单数据提交

### 作为 HTML 的内容

	<div> %content% </div>

HTML中 `<` `>` `&` 等有特殊含义（ `<` `>` 用于标签，`&` 用于转义），不能直接使用。如果你不希望自己写的 `<xxx>` 被当做标签解析，就需要做转换为对应的字符实体（或者实体编号）。

```
显示 |字符实体  | 实体编号
<   |&amp;lt;  |&amp;\#60;
>   |&amp;gt;  |&amp;\#62;
&   |&amp;amp; |&amp;\#38;
"   |&amp;quot;|&amp;\#34;
'   |&amp;apos;|&amp;\#39;
```

上面这 5 个转义是浏览器必须支持的。完整列表见[这里][1]。

举例来说，如果你想在 HTML 页面里显示 `&amp;` 这 5 个字符，直接在 HTML 代码里写 `&amp;`，你会在浏览器中只看见一个 `&` ；你只能在 HTML 代码里写 `&amp;amp;`。

再比如，你想在页面中显示 `<hello tag>`，那么代码里应该写 `&lt;hello tag&gt;`。

### 作为 JS 的内容（尤其是字符串）

	<script>var test = '%content%' ;</script>

显然 %content% 中出现引号会引发问题，所以我们需要把 `'` 和 `"` 替换为 `\'` 和 `\"`。

另外如果 %content% 中出现 `\` 则会把后面的字符给转义了，所以也要替换。如果 %content% 中出现 `*/` 则可能会影响原本的的注释，所以 `/` 要替换为 `\/` 。

显示    | 代码
\-------|--------
"      |\"  
'      |\'
\      |\\\\
/      |\/

### 作为 innerHTML

	<div id="test"></div> 
	
	<script>
	var content = '%content%';
	document.getElementById('test').innerHTML = content; 
	</script>

首先 %content% 是作为 JS 的内容，所以需要对 `"` `'` `\` `/`进行转义。其次它才作为 HTML 的内容，对`<` `>` `&` `"` `'` 进行转义。

### 作为 URL

	<iframe src="%content%"></iframe>

这个前端同学都知道，使用 `encodeURI` 方法将字符串变为可用的 URL 即可： （下面一行是转义后的结果）

	~ ! @ # $ %   ^   & * ( ) {   }   [   ]   = : / , ; ? + ' "   \   
	~ ! @ # $ %25 %5E & * ( ) %7B %7D %5B %5D = : / , ; ? + ' %22 %5C

### 作为 URL 的组件（URIComponent）

	<iframe src="http://qq.com/index.html?p=%content%/"></iframe>

使用 `encodeURIComponent` 方法：

	~ ! @   #   $   %   ^   &   * ( ) {   }   [   ]   =   :   /   ,   ;   ?   +   ' "   \
	~ ! %40 %23 %24 %25 %5E %26 * ( ) %7B %7D %5B %5D %3D %3A %2F %2C %3B %3F %2B ' %22 %5C

### 作为表单数据提交

form 表单的 enctype 属性规定了在发送到服务器之前应该如何对表单数据进行编码。默认地，表单数据会编码为 "application/x-www-form-urlencoded"。就是说，在发送到服务器之前，所有字符都会进行编码（空格转换为 "+" 加号，特殊符号转换为 ASCII HEX 值）。

如果你给 form 表单加上 `enctype="text/plain"`，那么提交的数据就不会做任何编码。

[1]:	http://www.w3schools.com/tags/ref_entities.asp#gsc.tab=0