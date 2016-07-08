# 函数

####1.剩余参数（Rest parameters）

剩余参数会默认转为一个数组对象（可以不用类数组arguments了）。

使用如下：

    console.log('containsAll:'+ containsAll('i like banana!',"banana", "b", "nan"));
    function containsAll(haystack, ...needles){
        for(var needle of needles){
            if (haystack.indexOf(needle)=== -1){
                return false;
            }
        }
        return true;
    }

####2.默认参数（Default parameters）