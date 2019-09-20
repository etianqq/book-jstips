# 变量和作用域
####1.基本类型和引用类型
* 5种基本类型Null,Undefined,Boolean,Number,String都是按值访问的，可以在栈中保存实际的值。
* Object是引用类型的值，在栈中保存的是引用类型的地址，而实际值存储在堆中。引用类型是按照引用访问的。

####2.复制变量
如果是基本类型，复制时，会在变量对象上创建一个新值，然后把该值复制到为新变量分配的位置上。

```var num1=5;```
```var num2=num1;```

     ---------------------------------
     |    num1     |      5     |
     ---------------------------------
     复制后
     ---------------------------------
     |    num1     |      5     |
     ---------------------------------
     |    num2     |      5     |
     ----------------------------------
     
如果是引用类型复制，那么复制的引用地址（指针），两个变量实际上引用的是同一个对象。
![](/assets/copy_obj.png)

####3.传递参数
**所以函数的参数都是按照值传递的。**也就是说，把函数外部的值**复制**给函数内部的参数。

例子：

      function addTen(num){
        num += 10;
        return num;
      }
      
      var count = 20;
      var result = addTen(count);
      alert(count);    //20
      alert(result);   //30
      
      -------------------------
     function setName(obj){
       obj.name = 'Nicole';
     } 
     var person = new Object(); // or 'var person = new String();'
     setName(person);
     alert(person.name);   // Nicole
      -------------------------
     function setName(obj) {
       obj.name = 'Nicole';
       obj = new Object();
       obj.name = 'Bill';
     }
     var person = new Object();
     setName(person);
     alert(person.name); // Nicole