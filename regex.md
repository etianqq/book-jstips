#正则表达式

####1. 定义正则表达式

* 是使用字面量，以斜杠表示开始和结束(**编译时新建正则表达式**)。
```
var reg1 = /hello \w{3,12}/g;
```
* 使用RegExp构造函数(**运行时新建正则表达式**)
```
var reg2 = new RegExp("hello \\w{3,12}",'g');
```

####2. 正则对象的属性和方法

######2.1 属性

* ignoreCase：返回一个布尔值，表示是否设置了i修饰符，该属性只读。
* global：返回一个布尔值，表示是否设置了g修饰符，该属性只读。
* multiline：返回一个布尔值，表示是否设置了m修饰符，该属性只读。

#######2.2 常用方法

* test(): 检索字符串中指定的值。返回 true 或 false
* exec(): 检索字符串中指定的值。匹配成功返回一个数组，匹配失败返回null。

####3. 支持正则表达式的 String 对象的方法

* search：在字符串内检索指定的值,匹配成功返回第一个匹配成功的字符串片段开始的位置，否则返回-1
```
var reg=/javascript/i;
console.log('hello Javascript Javascript Javascript'.search(reg));//6
```	
* match：在字符串内检索指定的值,匹配成功返回存放匹配结果的数组，否则返回null。如果没有设置全局匹配g，返回的数组只存第一个成功匹配的值。	
```
var reg1=/javascript/i;
var reg2=/javascript/ig;
console.log('hello Javascript Javascript Javascript'.match(reg1));
//['Javascript']
console.log('hello Javascript Javascript Javascript'.match(reg2));
//['Javascript','Javascript','Javascript']
```
* replace：替换与正则表达式匹配的子串，并返回替换后的字符串。在不设置全局匹配g的时候，只替换第一个匹配成功的字符串片段。
```
var reg1=/javascript/i;
var reg2=/javascript/ig;
console.log('hello Javascript Javascript Javascript'.replace(reg1,'js'));
//hello js Javascript Javascript
console.log('hello Javascript Javascript Javascript'.replace(reg2,'js'));
//hello js js js
```
* split：把字符串分割为字符串数组。
```
var reg=/1[2,3]8/;
console.log('hello128Javascript138Javascript178Javascript'.split(reg));
//['hello','Javascript','Javascript178Javascript']
```

字符串的match方法与正则对象的exec方法非常类似：匹配成功返回一个数组，匹配失败返回null。

如果正则表达式带有g修饰符，则该方法与正则对象的exec方法行为不同，会一次性返回所有匹配成功的结果。
```
var s = 'abba';
var r = /a/g;

s.match(r) // ["a", "a"]
r.exec(s) // ["a"]
```