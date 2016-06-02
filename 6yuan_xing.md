# 6.原型

**什么是原型？**

原型是一个对象，其他对象可以通过它实现属性继承。

**任何一个对象都可以成为原型么？**

是

**哪些对象有原型**

所有的对象在默认的情况下都有一个原型，因为原型本身也是对象，所以每个原型自身又有一个原型(只有一种例外，默认的对象原型在原型链的顶端)

http://blog.jobbole.com/9648/
http://www.jb51.net/article/30750.htm

####prototype

    function Foo(){}
    Foo.prototype; // 这个对象是在调用new Foo()时创建的，最后会被关联到这个“Foo.prototype”对象上
    Object.getPrototypeOf(a) === Foo.prototype;	//true
    
####原型继承