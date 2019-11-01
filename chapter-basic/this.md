#this对象
    function foo(){
        var a = 2;
        this.bar();
    }
    function bar(){
        console.log(this.a);
    }
    foo();	// ReferenceError: a is not defined


this是在**运行时进行绑定**的，并不是在编写时绑定，它的上下文取决于函数调用时的各种条件。
this的绑定和函数声明的位置没有任何关系，只取决于**函数的调用方式**。

####this绑定规则
1. 默认绑定:独立函数调用
```
function foo(){};
foo(); // this--->window
```
2. 隐式绑定:需要考虑调用位置是否有上下文
```
function foo(){
    console.log(this.a);
}
var obj2 = {a:2, foo: foo};
var obj1 = {a:1, obj2:obj2};
obj1.obj2.foo(); //2;
```
**对象属性引用链中只有上一层或者说最后一层在调用位置中起作用**
3. 显示绑定: call(),apply(),bind()
```
function foo(){	
    console.log(this.a);
}
var obj = {a:2};
foo.call(obj);	// 2 
```
在调用```apply```和```call```时会立即调用目标函数，而在调用```bind```时则不会如此，而是会返回一个函数（闭包）。
4. new绑定
```
function foo(a){
    this.a = a;
}
var bar = new foo(2);
bar.a; // 2    
```
使用```new```来调用函数，或者说发生构造函数调用时，会执行下面的操作：
    *  创建一个全新的对象
    * 这个新对象会被执行[[prototype]]连接
    * 这个新对象会绑定到函数调用的```this```
    * 如果函数没有返回其他对象，那么new表达式中的函数调用会自动返回这个新对象 

####绑定优先级从高到低

new 操作(```new Obj()```)->显式绑定(```obj.foo.call(obj2)```)->隐式绑定(```obj.foo()```)->默认绑定