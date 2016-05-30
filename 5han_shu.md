# 5.函数

####arguments
函数实际上是访问了函数体中一个名为 arguments 的内部对象，这个对象就如同一个**类似于数组**的对象一样，包括了所有被传入的参数。

>      function avg() {
> 
>       var sum = 0;
>    
>       for (var i = 0, j = arguments.length; i < j; i++) {
>    
>           sum += arguments[i];
>       }
>    
>       return sum / arguments.length;
>       }
> 
> avg(2, 3, 4, 5); // 3.5
> 
> avg.apply(null, [2, 3, 4, 5]); // 3.5
> 
> avg.call(null, 2, 3, 4, 5); // 3.5

####作用域