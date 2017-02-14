#属性描述符

例子：
```
var obj = {a: 2};
Object.getOwnPropertyDescriptor(obj, "a");
// Object {value: 2, writable: true, enumerable: true, configurable: true}

Object.defineProperty(obj, "b", {
    value: 3,           //值
    writable: true,     //可修改
    enumerable: true,   //可枚举
    configurable: true  //可配置
})
```
注意，当```configurable:false```的时候：
* writable可以由true改为false，但是无法由false改为true
* 该属性不能被删除

####如何设置一个常量
```
var obj = {a:3};

Object.preventExtensions(obj); // 禁止给对象添加新属性
Object.seal(obj);  //应用Object.preventExtensions，并且configurable:false
Object.freeze(obj); //应用Object.seal，并且writable: false

```

