#HTML集合

HTML集合是用于**存放DOM节点引用**的**类数组**对象；

* document.getElementsByName() 
* document.getElementsByClassName() 
* document.getElementsByTagName()
* document.images
* document.links
* document.forms
* document.forms[0].elements

注意两点：
1. 返回值是一个类数组
2. 返回值是一个对象引用，意味着，当底层文档对象更新时，它也会同步更新

看下面的例子：
```
var alldivs = document.getElementsByTagName('div'); 
for (var i = 0; i < alldivs.length; i++) { 
  document.body.appendChild(document.createElement('div')) 
}
```
该程序会陷入死循环，因为alldivs.length在每次迭代时都会增加。
