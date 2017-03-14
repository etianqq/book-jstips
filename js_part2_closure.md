
 # 闭包

理解闭包之前，需要理解函数作用域链！！！

查看下面的例子和图示：
```
function assignEvents(){
   var id = "xdi9592";
   document.getElementById("save-btn").onclick = function(event){
    saveDocument(id);
   };
}
```

 
 ####闭包定义

```
闭包，指的是一种特殊函数，这种函数会在被调用时保持当时的变量名查找的执行环境

（注：出自《JavaScript编程全解 [（日）》一书）。
```

**  
1. 闭包是什么？答：一种特殊函数。
2. 闭包特点是什么？答：被调用时，保留其定义时候的作用域执行环境。
** 
 闭包是在某个作用域内定义的函数，它可以访问这个作用域内的所有变量。

    function foo(){
        var a = 2;
        function bar(){
          console.log(a);
        }
        return bar;
    }
    var baz = foo();
    baz();	//	2	

闭包作用域链通常包括三个部分：

1. 函数本身作用域。
2. 闭包定义时的作用域。
3. 全局作用域。


闭包常见用途：

1. 创建特权方法用于访问控制
2. 事件处理程序及回调
