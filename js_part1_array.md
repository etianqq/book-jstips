# 数组
| 方法名称 | 描述 |
| -- | -- |
| a.toString() | 返回一个包含数组中所有元素的字符串，每个元素通过逗号分隔 |
| a.toLocaleString() | 根据宿主环境的区域设置，返回一个包含数组中所有元素的字符串，每个元素通过逗号分隔 |
| a.concat(item1[, item2[, ...[, itemN]]]) | 返回一个数组，这个数组包含原先 a 和 item1、item2、……、itemN 中的所有元素 |
| a.join(sep) | 返回一个包含数组中所有元素的字符串，每个元素通过指定的 sep 分隔 |
| a.pop() | 删除并返回数组中的最后一个元素。 |
| a.push(item1, ..., itemN) | 将 item1、item2、……、itemN 追加至数组 a |
| a.reverse() | 数组逆序（会更改原数组 a） |
| a.shift() | 删除并返回数组中第一个元素 |
| a.slice(start, end) | 返回子数组，以 a[start] 开头，以 a[end] 前一个元素结尾 |
| a.sort([cmpfn]) | 	依据 cmpfn 返回的结果进行排序，如果未指定比较函数则按字符顺序比较（即使元素是数字 |
| a.splice(start, delcount[, item1[, ...[, itemN]]]) | 从 start 开始，删除 delcount 个元素，然后插入所有的 item |
| a.unshift([item]) | 将 item 插入数组头部，返回数组新长度（考虑 undefined |

ES5中添加的迭代方法有：

| 方法名称 | 描述 |
| -- | -- |
| every | 每一项为true，返回true |
| filter | 返回原数组的一个子集 |
| forEach | 遍历数组，改变原数组 |
| map | 遍历数组，根据条件返回**新数组** |
| some | 有一项为true，返回true |
| reduce| 收一个函数作为累加器（accumulator），数组中的每个值（从左到右）开始合并，最终为一个值 |

ES6遍历数组值的方法：```for...of```

    var myArray = [1,2,3];
    for (var v of myArray){	
        console.log(v);
    }
    //1, 2, 3

####splice

    array.splice(start, deleteCount[, item1[, item2[, ...]]])

参数：

* start: 从数组的哪一位开始修改内容。如果超出了数组的长度，则从数组末尾开始添加内容；如果是负值，则表示从数组末位开始的第几位。
* deleteCount: 整数，表示要移除的数组元素的个数。如果 deleteCount 是 0，则不移除元素。这种情况下，至少应添加一个新元素。如果 deleteCount 大于start 之后的元素的总数，则从 start 后面的元素都将被删除（含第 start 位）。
* itemN: 要添加进数组的元素。如果不指定，则 splice() 只删除数组元素。

####reduce

    arr.reduce(callback,[initialValue])

* callback：执行数组中每个值的函数，包含四个参数
  * previousValue:上一次调用回调返回的值，或者是提供的初始值（initialValue）
  * currentValue: 数组中当前被处理的元素
  * index: 当前元素在数组中的索引
  * array: 调用 reduce 的数组
* initialValue: 作为第一次调用 callback 的第一个参数。

注意：

1. 如果数组为空并且没有提供initialValue， 会抛出TypeError 。

2. 如果数组仅有一个元素（无论位置如何）并且没有提供initialValue， 或者有提供initialValue但是数组为空，那么此唯一值将被返回并且callback不会被执行。

参考：
* [https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/splice](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/splice)
* [https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/Reduce](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/Reduce)

####isArray
判断对象是否为数字``Array.isArray(myArray)``

Polyfill:

    if(typeof Array.isArray === 'undefined'){
      Array.isArray = function(arg){
      return Object.prototype.toString.call(arg) === '[object Array]';
      }
    }

