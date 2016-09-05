# 客户端存储
####1. cookie

* 如果 cookie 不包含到期日期，则可视为会话 cookie。 会话 cookie 存储在内存中，决不会写入磁盘。 当浏览器关闭时，cookie 将从此永久丢失。
* 如果 cookie 包含到期日期，则可视为持久性 cookie。 在指定的到期日期，cookie 将从磁盘中删除。

####2. localStorage
用于在客户端存储较长时间的数据，一个简单的例子就是用于记录某用户访问该页面的次数。当页面采用Local Storage存储，其被关闭并再次打开后，先前存储的数据仍然存在。

#####保存和获取数据

```localStorage.setItem(1, 'The data is stored local from csser.com');```
然后可以这样获取：

```var data = localStorage.getItem(1);```

#####清空数据

同样，Local Storage支持length属性、removeItem()和clear()。

对于Session Storage和Local Storage，clear()函数的目的是相同的—都用于清空列表中的数据，这意味着一旦调用了它，比如localStorage.clear()，它将删除所有同源的本地存储数据，因此所有Local Storage数据都会被清空，像www.csser.com、www.csser.com:80、www.csser.com/category/share/、www.csser.com/category/dev/等.

####3. sessionStorage
存储当前会话的所有数据，当你关掉窗口或者标签时立刻丢掉这些数据。

#####数据的保存和获取

保存```sessionStorage.setItem(yourkey, yourvalue);```
获取```var item = sessionStorage.getItem(yourkey);```
通过一行简单的语句向Session Storage存储数据：

#####删除数据

```var item = sessionStorage.removeItem(yourkey);```

clear()方法用于清空整个列表的所有数据，可以这样使用：
```sessionStorage.clear();```