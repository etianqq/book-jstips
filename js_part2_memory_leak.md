# js内存泄漏

####1.对象之间的相互引用

对于纯粹的 ECMAScript 对象而言，只要没有其他对象引用对象 a、b，也就是说它们只是相互之间的引用，那么仍然会被垃圾收集系统识别并处理。

但是，在 Internet Explorer 中，如果循环引用中的任何对象是 DOM 节点或者 ActiveX 对象，垃圾收集系统则不会发现它们之间的循环关系与系统中的其他对象是隔离的并释放它们。最终它们将被保留在内存中，直到浏览器关闭。

如果两个对象A，B彼此引用，并且有第三方对象C保留其中一个对象的引用时，可能会造成A或者B对象无法被释放。

####2.闭包
这个情况会比较多，如果闭包对象引用了父函数的变量对象，那么，哪怕父函数引用置为null，该父函数对象依然无法被垃圾回收掉。

        function bindEvent() 
        { 
            var obj=document.createElement("XXX"); 
            obj.onclick=function(){ 
              //Even if it's a empty function 
            } 
        }
    
闭包可以维持函数内局部变量，使其得不到释放。

上例定义事件回调时，由于是函数内定义函数，并且内部函数--事件回调的引用外暴了，形成了闭包

解决之道，将事件处理函数定义在外部，解除闭包

      function bindEvent() 
      { 
          var obj=document.createElement("XXX"); 
          obj.onclick=onclickHandler; 
      } 
      function onclickHandler(){ 
          //do something 
      }
或者在自定义函数里面删除对Dom的引用

      function bindEvent() 
       { 
          var obj=document.createElement("XXX"); 
          obj.onclick=function(){ 
                //Even if it's a empty function 
            } 
          obj=null; 
      }