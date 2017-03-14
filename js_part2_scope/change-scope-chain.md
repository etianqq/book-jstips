#改变作用域链的语句

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

