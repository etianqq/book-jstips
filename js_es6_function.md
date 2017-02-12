# 函数

####1.剩余参数（Rest parameters）

剩余参数会默认转为一个数组对象（可以不用类数组arguments了）。

使用如下：

    console.log('containsAll:'+ containsAll('i like banana!',"banana", "b", "nan"));  // containsAll:true
    function containsAll(haystack, ...needles){
        for(var needle of needles){
            if (haystack.indexOf(needle)=== -1){
                return false;
            }
        }
        return true;
    }

* 只有位于最末的参数可被标记为剩余参数。
* 位于剩余参数之前的参数与普通参数的处理方式是一样的。
* 所有的额外参数都会被放入一个数组然后再分配给剩余参数。如果没有额外参数，剩余参数则为一个空数组；
* 剩余参数不能被赋值为undefined。

####2.默认参数（Default parameters）
使用如下：

    animalSentence();   //Lions and tigers and bears! Oh my!
    animalSentence('cat', 'bear');    //Lions and cat and bear! Oh my!

    function animalSentence(animals2="tigers", animals3="bears") {
        console.log(`Lions and ${animals2} and ${animals3}! Oh my!`);
    }
    
* 取值undefined的作用等于是没有传入任何东西。因此，animalSentence(undefined, "unicorns") 返回的是 "Lions and tigers and unicorns! Oh my!"
* 没有显式定义的默认参数等同于undefined。`function func(a=1,b)`等价于`function func(a=1,b=undefined)`

####3.箭头函数（Arrow functions）
可以省略function, return（某些情况下）,括号和分号。

    // ES5  
    var total = values.reduce(function (a, b) {  
      return a + b;  
    }, 0);  
    
    // ES6  
    var total = values.reduce((a, b) => a + b, 0); 
    
    setTimeout(()=> {
        console.log(this.name);
    }, 100);
    
**箭头函数没有自己的this值，其this值是根据外层（函数或者全局）作用域来决定的。**

