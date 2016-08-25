##对象
####创建对象
JavaScript 中的对象可以简单理解成“名称-值”对，有两种简单方法可以创建一个空对象：

1.```var obj = new Object();```

    function Person(name, age) {
      this.name = name;
      this.age = age;
    }
    var person = new Person("nicole", 24);
    console.log(person.name);  // 'nicole'

2.```var obj = {}; // 对象字面量（object literal）```

####原型(prototype)

每一个javascript对象(null除外)都会和另外一个对象相关(prototype)。
可以通过obj.prototype获得原型对象的引用。
后续将有一章专门讲对象原型。

####访问对象属性

对象的属性可以通过链式（chain）表示方法进行访问：

1.```obj.details.color; // orange```

2.```obj["details"]["size"]; // 12```

第二种方法的优点：属性的名称被看作一个字符串，这就意味着它可以在**运行时被计算**。

####删除对象属性

```delete obj.propertyName```

####枚举属性
```for(var key in obj)```
如果只是枚举对象的自定义属性，需要加上checking condition: ```obj.hasOwnProperty(p)```

####属性的getter和setter(存储器属性)

上面讲到的都是‘数据属性’（数据属性只有一个简单的值）。

和‘数据属性’不同，**存储器属性**不具有可写性。如果属性同时具有getter和setter方法，那么它是一个读/写属性；如果只有getter，那就是只读属性；如果只有setter，那就是只写属性。

     var p = {
        x: 1,  
        y: 2,
        get r() {
            return this.x + this.y;
        },
        set r(ratio) {
            this.x = ratio * this.x;
            this.y = ratio * this.y;
        },
        get s() {
            return this.x * this.y;
        }
    };

    p.r = 4;
    p.s = 5;
    console.log(p.r);  //12
    console.log(p.s);  //32

####属性描述符
除了包含名字和值之外，属性还包含一些标识它们可写，可枚举，可配置的特性。在ES3中无法设置这些特性。

从ES5开始，所有的属性都具备了属性描述符。

    var myObject={	
		a:2
    };
    Object.getOwnPropertyDescriptor(myObject,"a");	
    //	{
    //	  value:	2,
    //      writable:	true,  //是否可修改
    //	  enumerable:	true, //是否在for...in循环中出现
    //	  configurable:	true //修改一个不可配置的属性描述符会出错
    //	}
    
在创建普通属性时属性描述符会使用默认值，我们也可以使用Object.defineProperty(..)来添加
一个新属性或者修改一个已有属性（如果它是configurable）并对特性进行设置。

    var myObject = {};
    Object.defineProperty( myObject,"a",{
			value: 2,
			writable: false,	
			configurable: true,	
			enumerable: true
    }	);	
    myObject.a = 3;
    myObject.a;	// 2
    
如果只定义value，那么其他属性特性为false。

    var o ={};
    Object.defineProperty(o,'x'{value:1});
    Object.getOwnPropertyDescriptor(o,'x');

    ==>Object {value: 1, writable: false, enumerable: false, configurable: false}

使用场景，比如声明一个常量。

```Object.seal(..)```会创建一个“密封”的对象，这个方法实际上会在一个现有对象上
用Object.preventExtensions(..)并把所有现有属性标记为configurable:false。

```Object.freeze(..)```会创建一个冻结对象，这个方法实际上会在一个现有对象上调
用Object.seal(..)并把所有“数据访问”属性标记为writable:false，这样就无法修改它们的值。
