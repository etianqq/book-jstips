#作用域和作用域链

####1. 作用域（也称为执行上下文）
一句话简述**“作用域”**---“执行JavaScript代码时，JavaScript引擎会创建一个执行上下文，它设定了代码执行时所处的环境”。


当页面加载完：

1. 创建一个全局的执行上下文（this指向我们熟知的window）；
2. 每执行一个JavaScript函数，都会创建一个对应的执行上下文；
3. 函数里面可能执行嵌套函数......继续创建子函数的执行上下文；
4. 最终，会创建出一个栈，当前作用域在栈顶，全局作用域在栈底；


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

当try代码块中发生错误，执行过程会自动跳转到catch子句，然后**把异常对象推入一个变量对象并置于作用域首位**。此时，函数所有局部变量都会放在第二个作用域对象中。

