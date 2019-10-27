###  排序算法

公共函数

```javascript
function checkArray(array) {
    if (!array) return
}
function swap(array, left, right) {
    let rightValue = array[right]
    array[right] = array[left]
    array[left] = rightValue
}
```



#### 冒泡排序

1. 从第一个元素开始，把当前元素和下一个比较，如果当前元素较大，就互换位置，重复操作到最后一个元素。

2. 这时，最后一个元素一定是最大的。

3. 重复步骤1，但是只需要比较到`len - 2`位置。
4. 重复n次

```javascript
function bubble(array) {
  checkArray(array);
  for (let i = array.length - 1; i > 0; i--) {
    // 从 0 到 `length - 1` 遍历
    for (let j = 0; j < i; j++) {
      if (array[j] > array[j + 1]) swap(array, j, j + 1)
    }
  }
  return array;
}

例子：
54321
43215
32145
21345
12345
```

特点：每轮循环都能找到最大的数字

复杂度：O(n*n)



####  插入排序

1. 第一个是默认已排序元素。
2. 外层指针N依次后移到一位。内层指针指向N-1位置，然后比较内层N-1和N，如果N-1较大，则交换。
3. 如果此时N-1>0，内层指针左移一位，比较N-2和N-1，如果N-2较大，则交换。
4. 重复步骤3
5. 步骤遍历完毕，再重复步骤2+3

```javascript
function insertion(array) {
  checkArray(array);
  for (let i = 1; i < array.length; i++) {
    for (let j = i - 1; j >= 0 && array[j] > array[j + 1]; j--)
      swap(array, j, j + 1);
  }
  return array;
}

例子：
321
231
213
123
```

特点：每轮循环都能找到最小的数字

复杂度：O(n*n)



#### 选择排序

1. 设置最小值索引为0。
2. 遍历数组，如果取出的值比索引值小，就替换最小索引值
3. 此时，第一个元素是最小值
4. 然后从设置最小索引为1，重复2-3

```
function selection(array) {
  checkArray(array);
  for (let i = 0; i < array.length - 1; i++) {
    let minIndex = i;
    for (let j = i + 1; j < array.length; j++) {
      minIndex = array[j] < array[minIndex] ? j : minIndex;
    }
    swap(array, i, minIndex);
  }
  return array;
}

例子
4321
1324
1234
```

特点：每轮循环都能找到最小的数字

复杂度：O(n*n)



