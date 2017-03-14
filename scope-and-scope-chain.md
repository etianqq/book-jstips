#作用域和作用域链

####1. 作用域（也称为执行上下文）
一句话简述**“作用域”**---“执行JavaScript代码时，JavaScript引擎会创建一个执行上下文，它设定了代码执行时所处的环境”。


当页面加载完：

1. 创建一个全局的执行上下文（this指向我们熟知的window）；
2. 每执行一个JavaScript函数，都会创建一个对应的执行上下文；
3. 函数里面可能执行嵌套函数......继续创建子函数的执行上下文；
4. 最终，会创建出一个栈，当前作用域在栈顶，全局作用域在栈底；

####2. 作用域链
**每个执行上下文都有一个与之关联的作用域链**。
当函数被创建时（注意，不是执行），JavaScript引擎会把**创建时执行上下文的作用域链**赋给函数内部属性```[Scope]```。

**[Scope]指向一个对象，其包含了一个函数被创建的作用域中对象的集合，此集合被称为函数的作用域链（作用域链决定哪些数据能够被函数访问）**

作用域链：
1. 创建函数时，插入全局对象
2. 执行函数时，JavaScript引擎创建一个活动对象（Active object），添加到作用域链顶部（函数每次执行时对应的执行环境都是独一无二的，多次调用同一个函数会创建多个执行环境。当函数执行完毕，执行环境被销毁）。


用一个例子做进一步说明：
```
function add(num1, num2){
  var sum = num1 + num2;
  return sum;
}

var total = add(5, 10);
```

![scope chain.jpg](http://upload-images.jianshu.io/upload_images/25750-8bc1fad8334d6a01.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

执行上面的JavaScript代码，但还没有执行add函数时，add函数scope chain只有一个值，指向global object。
然后，执行add函数，一个活动对象被创建，并且被加到scope chain顶部。
由此，执行add函数时，一个两层的作用域链被建立。

