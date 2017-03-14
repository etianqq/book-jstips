#原型链

基本思想：利用原型让一个引用类型继承另一个引用类型的属性和方法。

######构造函数，原型和实例的关系

* 每个构造函数都有一个指向原型对象的属性（prototype）；
* 原型对象都包含一个指向构造函数的指针（constructor）；
* 实例都包含一个指向原型对象的内部指针（__proto__）；

如果在第一个对象上没有找到需要的属性或者方法引用，引擎就会继续在[[prototype]]关联的对象上进行查找。同理，如果在后者也没有找到需要的引用，就会继续查找它的[[prototype]]，以此类推。

下面是一个例子：
```
    function SuperType() {
        this.property = true;
    }

    SuperType.prototype.getSuperValue = function () {
        return this.property;
    };

    function SubType() {
        this.subproperty = false;
    }

    SubType.prototype = new SuperType();

    SubType.prototype.getSubValue = function () {
        return this.subproperty;
    };

    var instance = new SubType();
```

![](/assets/prototype.png)