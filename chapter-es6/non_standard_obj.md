# 非标准库对象

####1.Map
使用方法：

    var map = new Map();  
    map.set(window, "the global");  
    map.set(document, "the document");  
  
    for (var [key, value] of map) {  
      console.log(key + " is " + value);  
    } 

就像一个普通对象,通过key值来设置value。它与Object最大的区别是：
* 对象含有原型对象属性prototype，但是Map没有
* 普通对象中，key只能是string；Map的key值，可以是string或者Symbols
* 可以通过map.size()取得长度;普通对象没有这个方法

但是并不是所有情况都适应用Map，大部分情况还是用简单对象。

如果出现下面的情况，可以考虑使用Map:
* Are keys usually unknown until run time, do you need to look them up dynamically?
* Do all values have the same type, and can be used interchangeably?
* Do you need keys that aren't strings?
* Are key-value pairs often added or removed?
* Do you have an arbitrary (easily changing) amount of key-value pairs?
* Is the collection iterated?

更多例子： 
1. [https://jsfiddle.net/etianqq/7c6f875y/](https://jsfiddle.net/etianqq/7c6f875y/)
2. https://jsfiddle.net/etianqq/y0gog6h2/