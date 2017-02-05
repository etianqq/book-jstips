#performance.now()

* ```performance.now()``` 与 ```Date.now()``` 不同的是，返回了以微秒（百万分之一秒）为单位的时间，更加精准。
* 并且与 ```Date.now()``` 会受系统程序执行阻塞的影响不同，```performance.now()``` 的时间是以恒定速率递增的，不受系统时间的影响（系统时间可被人为或软件调整）。
* 注意 ```Date.now()``` 输出的是 UNIX 时间，即距离 1970 的时间，而 ```performance.now()``` 输出的是相对于 ```performance.timing.navigationStart```(页面初始化) 的时间。

#####使用 performance.mark() 也可以精确计算程序执行时间
使用 performance.mark() 标记各种时间戳（就像在地图上打点），保存为各种测量值（测量地图上的点之间的距离），便可以批量地分析这些数据了。

直接上示例代码看注释便明白：
```
function randomFunc (n) {  
    if (!n) {
        // 生成一个随机数
        n = ~~(Math.random() * 10000);
    }
    var nameStart = 'markStart' + n; 
    var nameEnd   = 'markEnd' + n; 
    // 函数执行前做个标记
    window.performance.mark(nameStart);
 
    for (var i = 0; i < n; i++) {
        // do nothing
    }
 
    // 函数执行后再做个标记
    window.performance.mark(nameEnd);
 
    // 然后测量这个两个标记间的时间距离，并保存起来
    var name = 'measureRandomFunc' + n;
    window.performance.measure(name, nameStart, nameEnd);
}
 
// 执行三次看看
randomFunc();  
randomFunc();  
// 指定一个名字
randomFunc(888);
```
[参考文章:初探 performance – 监控网页与程序性能](http://www.alloyteam.com/2015/09/explore-performance/)