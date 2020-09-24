## ES6 基础练习题

#### 1. 手写一个迭代器generator函数

调用如下：
```
const it = makeIterator(['人月', '神话']);
console.log(it.next()); // { value: "人月", done: false }
console.log(it.next()); // { value: "神话", done: false }
console.log(it.next()); // {value: undefined, done: true }
```







### 答案
```
const makeIterator = arr => {
  let nextIndex = 0;
  return {
    next: () =>
      nextIndex < arr.length
        ? { value: arr[nextIndex++], done: false }
        : { value: undefined, done: true },
  };
};
```