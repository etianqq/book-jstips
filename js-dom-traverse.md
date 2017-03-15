#遍历DOM

* childNode：获得元素集合
* nextSibling：获得元素的相邻元素

上述两种方法并不区分元素节点和其他类型节点（比如注释和文本节点）。

如果只需要访问元素节点，建议使用下图左列的方法：

![](/assets/dom selector.png)

####选择器API：querySelectorAll()

建议使用```querySelectorAll```，它查找元素要快很多。优点如下：

1. 返回值为数组
2. 因此返回的节点不会对应实时的文档结构

