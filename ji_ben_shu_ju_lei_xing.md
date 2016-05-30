# 数据类型

JavaScript 中的类型应该包括这些：

* Number（数字）
* String（字符串）
* Boolean（布尔）
* Symbol（符号）（第六版新增）
* Object（对象）
  * Function（函数）
  * Array（数组）
  * Date（日期）
  * RegExp（正则表达式）
* Null（空）
* Undefined（未定义）


Tips: 
1. JavaScript 中 null 和 undefined 是不同的，前者表示一个空值（non-value），必须使用null关键字才能访问，后者是“undefined（未定义）”类型的对象，表示一个未初始化的值，也就是还没有被分配的值。
2. JavaScript 允许声明变量但不对其赋值，一个未被赋值的变量就是 undefined 类型。还有一点需要说明的是，undefined 实际上是一个不允许修改的常量。
3. 简单类型的数据不要使用对象形式赋值。比如:```var a = 5;//ok  var a = Number(5); // not ok```
因为如果用对象的形式声明简单类型，会产生一个对应的实例，而，如果不手动销毁这个实例，会占用内存。
