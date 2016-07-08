# 解构赋值
解构赋值可将数组的元素或对象的属性赋予给另一个变量，该变量的定义语法与数组字面量或对象字面量很相似。

基本语法形式为`[ variable1, variable2, ..., variableN ] = array;`

如果用ES5，赋值如下：

    var first = someArray[0];  
    var second = someArray[1];  
    var third = someArray[2]; 
    
如果用ES6，赋值如下：

    var [first, second, third] = someArray;  

####解构数组

    var [,,third] = ["foo", "bar", "baz",'test','hello'];
    console.log(third);  //baz
    var [arg1,...array] = ["foo", "bar", "baz",'test','hello'];
    console.log(arg1);   //foo
    console.log(array);   // ["bar", "baz",'test','hello']
    
####解构对象
在对象中使用解构赋值，允许你为对象的不同属性绑定变量名。

解构赋值的左侧部分类似一个对象字面量，对象中是一个名值对的列表，属性名称位于名值对内冒号左侧，变量名称位于名值对内冒号右侧，每一个属性都会去右侧对象中查找相应的赋值，每一个值都会赋值给它对应的变量。

    var { name: nameA } = robotA;
    var { name: nameB } = robotB;

    console.log(nameA); // "Bender"
    console.log(nameB); // "Flexo"