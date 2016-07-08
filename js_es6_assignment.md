# 解构赋值
解构赋值可将数组的元素或对象的属性赋予给另一个变量，该变量的定义语法与数组字面量或对象字面量很相似。

基本语法形式为`[ variable1, variable2, ..., variableN ] = array;`

如果用ES5，赋值如下：

    var first = someArray[0];  
    var second = someArray[1];  
    var third = someArray[2]; 
    
如果用ES6，赋值如下：

    var [first, second, third] = someArray;  

####数组解构赋值

    var [,,third] = ["foo", "bar", "baz",'test','hello'];
    console.log(third);  //baz
    var [arg1,...array] = ["foo", "bar", "baz",'test','hello'];
    console.log(arg1);   //foo
    console.log(array);   // ["bar", "baz",'test','hello']
    
