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
    
####非对象、数组、迭代的解构类型
1. 如果对Null/undefined使用解析赋值，会抛错。`var {error}=null;`
2. 对其他原始类型，如boolean,number,string,nan等运用解析赋值，会得到undefined。`var {nullstr}= NaN`。

####使用默认值
      
      var [missing = true] = []; // missing -> true
      var {message:msg = 'hello'} = {}; // msg -> 'hello'
      
####解构的实际应用
#####从CommonJS的模块中导入接口名
当导入一些CommonJS的模块时，非常常见的情况是模块的接口功能比你实际需求的多许多。通过解构的方式，你可以明确你需要的那部分，并且可以防止多余的接口名污染你的命名空间：

      const { SourceMapConsumer, SourceNode } = require("source-map");  
      
#####函数参数定义
作为开发人员，我们经常把一个对象用作函数的参数。这个对象具有很多的属性，以便暴露出更多便于我们使用的API，从而无需迫使我们的开发者去记住大量独立参数的顺序。我们对参数对象使用解构赋值，这样，在访问对象属性时，便可以避免重复调用这一参数对象，示例代码如下：

      function removeBreakpoint({ url, line, column }) {  
        // ...  
      }
      
#####配置对象参数
配置对象或是对象的属性已经有了合理的默认值时，如下：

    jQuery.ajax = function (url, {  
      async = true,  
      beforeSend = noop,  
      cache = true,  
      complete = noop,  
      crossDomain = false,  
      global = true,  
      // ... more config  
    }) {  
      // ... do stuff  
    }; 