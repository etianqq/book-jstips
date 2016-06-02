# this对象
    function foo(){
        var a = 2;
        this.bar();
    }
    function bar(){
        console.log(this.a);
    }
    foo();	// ReferenceError: a is not defined


this是在**运行时进行绑定**的，并不是在编写时绑定，它的上下文取决于函数调用时的各种条件。this的绑定和函数声明的位置没有任何关系，只取决于**函数的调用方式**。

改变this对象，call() 和 apply()。

    function foo(){	
        console.log(this.a);
    }
    var obj = {a:2};
    foo.call(obj);	// 2

绑定优先级从高到低：

new 操作(```new Obj()```)->显式绑定(```obj.foo.call(obj2)```)->隐式绑定(```obj.foo()```)->默认绑定