#组匹配

#### 1.概述

正则表达式的括号表示分组匹配，括号中的模式可以用来匹配分组的内容。
```
/fred+/.test('fredd') // true
/(fred)+/.test('fredfred') // true

var m = 'abcabc'.match(/(.)b(.)/);
m// ['abc', 'a', 'c']
```

######1.1 g 修饰符

**不使用```g```修饰符的时候，match可以获得分组内容。**
如果使用```g```修饰符，就无法获得分组内容。
```
'abcabc'.match(/(.)b(.)/g); //["abc", "abc"]
```
######1.2 \n匹配内容

在正则表达式内部，可以用```\n```引用括号匹配的内容，n是从1开始的自然数，表示对应顺序的括号。

下面是一个匹配网页标签的例子:
```
var tagName = /<([^>]+)>[^<]*<\/\1>/;
tagName.exec("<b>bold</b>")[1]
// 'b'
```

####2.非捕获组 (?:x)

(?:x)称为非捕获组（Non-capturing group），表示不返回该组匹配的内容，即匹配的结果中不计入这个括号。

非捕获组的作用请考虑这样一个场景，假定需要匹配foo或者foofoo，正则表达式就应该写成/(foo){1, 2}/，但是这样会占用一个组匹配。这时，就可以使用非捕获组，将正则表达式改为/(?:foo){1, 2}/，它的作用与前一个正则是一样的，但是不会单独输出括号内部的内容。

请看下面的例子。
```
var m = 'abc'.match(/(?:.)b(.)/);
m // ["abc", "c"]
```

####3.先行断言 x(?=y)

x(?=y)称为先行断言（Positive look-ahead），x只有在y前面才匹配，**y不会被计入返回结果**。比如，要匹配后面跟着百分号的数字，可以写成/\d+(?=%)/。

“先行断言”中，括号里的部分是不会返回的。

```
var m = 'abc'.match(/b(?=c)/);
m // ["b"]
```

####4. 先行否定断言 x(?!y)

x(?!y)称为先行否定断言（Negative look-ahead），x只有不在y前面才匹配，y不会被计入返回结果。比如，要匹配后面跟的不是百分号的数字，就要写成/\d+(?!%)/。

“先行否定断言”中，括号里的部分是不会返回的。
```
var m = 'abd'.match(/b(?!c)/);
m // ['b']
```