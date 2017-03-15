#DOM编程

文档对象模型（DOM）是一个独立于语言的，用于操作XML和HTML的程序接口。
尽管DOM是与语言无关的API，但它在浏览器中的接口使用JavaScript实现的。
浏览器中，会把DOM和JavaScript独立实现。

比如Chrome，
* DOM和渲染：webkit中的WebCore
* JavaScript：V8引擎

####开销
访问DOM元素代价是比较大的，修改元素更为昂贵，因为它会导致浏览器重新计算页面的变化，再次渲染。