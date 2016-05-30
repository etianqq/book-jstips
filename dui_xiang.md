# 对象
####创建对象
JavaScript 中的对象可以简单理解成“名称-值”对，有两种简单方法可以创建一个空对象：

1.```var obj = new Object();```

2.```var obj = {}; // 对象字面量（object literal）```

####原型(prototype)


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

####自定义对象


> function Person(name, age) {
> 
> this.name = name;
> 
> this.age = age;
> 
>}
>
> var person = new Person("nicole", 24);
>  
> console.log(person.name);  // 'nicole'