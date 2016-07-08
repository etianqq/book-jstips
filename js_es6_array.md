# 数组

####1.for...of
for-in语法是被设计来遍历普通的“键值对”对象的，不适合用在数组上。

for...of语法：

     for (var value of myArray) {   
        console.log(value);   
      }  
* 这是目前遍历数组最简洁和直接的语法；
* 它避免了for-in的所有缺陷；
* 与forEach()不一样，它支持break，continue和return。

####迭代器对象