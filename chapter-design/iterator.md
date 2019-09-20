# 迭代器模式

提供一个API来遍历或者操纵复杂的自定义数据结构

    var agg = (function () {
        var index = 0, data = [1, 2, 3, 4, 5], length = data.length;
        return {
            next: function () {
                var element;
                if (!this.hasNext()) {
                    return null;
                }
                element = data[index];
                index = index + 1;
                return element;
            },
            hasNext: function () {
                return index < length;
            }
        }

    }());

    //usage
    while (agg.hasNext()) {
        console.log(agg.next());
    }