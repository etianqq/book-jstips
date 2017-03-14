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

![](/assets/scope chain 1.jpg)

执行上面的JavaScript代码，但还没有执行add函数时，add函数scope chain只有一个值，指向global object。
然后，执行add函数，一个活动对象被创建，并且被加到scope chain顶部。
由此，执行add函数时，一个两层的作用域链被建立。

#### 3. 改变作用域链的语句

有两个语句可以改变作用域链，```with```和```try-catch```。

##### 1) with语句

用with改变函数作用域链：
```
function initUI(){
 with (document){ //avoid!
     var bd = body,
     links = getElementsByTagName_r("a"),
     i = 0,
     len = links.length;
     while(i < len){
         update(links[i++]);
     }
     getElementById("go-btn").onclick = function(){
         start();
     };
     bd.className = "active";
  }
}
```

当代码执行到with语句时，执行环境的作用域链临时被改变：**一个新的变量对象被创建**，其包含了参数指定对象的所属属性（如下图，with variable object）。

这时，函数的局部变量都处在第二个作用域链对象中，因此，访问代价更高了。

![](/assets/scope chain 2.png)


##### 2) try-catch语句


