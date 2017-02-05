#performance.memory（浏览器内存情况）

* jsHeapSizeLimit
* totalJSHeapSize
* usedJSHeapSize   

``` 
注：usedJSHeapSize表示所有被使用的js堆栈内存；
totalJSHeapSize表示当前js堆栈内存总大小。
这表示usedJSHeapSize不能大于totalJSHeapSize，如果大于，有可能出现了内存泄漏。
```

![](/assets/performance.memory.png)