#原型

JavaScript 中的对象是基于原形的。

原形是其他对象的基础，定义并实现了一个新对象所必须具有的成员。这一概念完全不同于传统面向对象编程中“类”的概念，它定义了创建新对象的过程。**原形对象为所有给定类型的对象实例所共享**，因此所有实例共享原形对象的成员。

一个对象通过一个内部属性绑定到它的原形（Firefox，Safari，和 Chrome 向开发人员开放这一属性，称作```__proto__```）。

因此，对象可以有两种类型的成员：实例成员（也称作“own”成员）和原形成员。
* 实例成员直接存在于实例自身
* 原形成员则从对象原形继承

参考例子：
```
var book = {
 title: "High Performance JavaScript",
 publisher: "Yahoo! Press"
};
alert(book.toString()); //"[object Object]"
```