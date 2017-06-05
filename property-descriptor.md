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
* 不能修改它的可配置性和可枚举性
* writable可以由true改为false，但是无法由false改为true
* 该属性不能被删除

https://segmentfault.com/a/1190000007290020

####如何设置一个常量
```
var obj = {a:3};

Object.preventExtensions(obj); // 禁止给对象添加新属性
Object.seal(obj);  //应用Object.preventExtensions，并且configurable:false
Object.freeze(obj); //应用Object.seal，并且writable: false

```

####getter和setter(存储器属性)
```
var obj = {
    get a(){
        return this._a_;
    }
    
    set a(val) {
        this._a_=val*2;
    }
}
obj.a = 2;
obj.a; // 4
```

####存在性
* ```key in obj```:检查属性key是否在对象obj或其原型链中
* ```obj.hasOwnProperty('key')```：检查属性key是否在对象obj中（不包含原型链）
* ```obj.propertyIsEnumerable('key')```：检查属性key是否在对象obj中（不包含原型链）,并且该属性enumerable: true
* ```Object.keys(obj)```:返回数组，包含所有可枚举的属性（不包含原型链）


