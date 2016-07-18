# 柯里化(curry)
柯里化就是一个函数的返回值也是一个函数，并且返回值函数需要使用宿主函数的参数，才可以完成自身的计算。

下面是一个通用curry化函数：

    function schonfinkelize(fn) {  
        var slice = Array.prototype.slice,  
        stored_args = slice.call(arguments, 1);  
        return function () {  
            var new_args = slice.call(arguments),  
            args = stored_args.concat(new_args);  
            return fn.apply(null, args);  
      };  
    }  

应用例子如下：

    // a curried add  
    // accepts partial list of arguments  
    function add(x, y) {  
      if (typeof y === "undefined") { // partial  
        return function (y) {  
            return x + y;  
        };  
      }  
      // full application  
      return x + y;  
    } 

调用：``add(3)(4); // 7``

####何时使用curry化
当你发现你调用同一个的函数，而传递的参数大部分都是一样的时候，那么这个参数就是一个很好的可以柯里化的候选函数。

你可以动态创建一个新函数，部分应用一组参数到你的函数。接着新函数会存储重复的参数(那么你就不用每次都传递)，并且会用它们去填充原始函数需要的参数列表。