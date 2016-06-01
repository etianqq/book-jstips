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

ES6遍历数组值的方法：```for...of```

    var myArray = [1,2,3];
    for (var v of myArray){	
        console.log(v);
    }
    //1, 2, 3
