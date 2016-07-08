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