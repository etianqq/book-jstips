# 练习题

#### 第1题
 
    console.log(a);
    var a = 3;    // undefined
    -----------------------
    console.log(a);
    a = 3;    // throw ReferenceError

#### 第2题：error

    foo();	// TypeError
    bar();	// ReferenceError
    var foo=function bar()	{...}

#### 第3题：闭包

    for (var i = 0; i < 10; i++) {  
        setTimeout(function () {
        alert('I am link #' + i);
      }, 100);
    }

#### 第4题: 函数

```
var a=1
var b=2; 
function test(a, b){
    var temp = a; 
    a = b; 
    b = temp; 
} 
test(a, b); 

console.log('a---'+ a);
console.log('b---'+ b);
```

```
var a={a: 1}
var b={b: 1}; 
function test(a, b){
    var temp = a; 
    a = b; 
    b = temp; 
} 
test(a, b); 

console.log('a---'+ JSON.stringify(a));
console.log('b---'+ JSON.stringify(b));
```
#### 第5题： event loop

```
console.log('start')

setTimeout(() => {
  console.log('setTimeout')
}, 0)

new Promise((resolve) => {
  console.log('promise')
  resolve()
})
  .then(() => {
    console.log('then1')
  })
  .then(() => {
    console.log('then2')
  })

console.log('end')
```

#### 第5题： event loop 2

```
console.log('script start')

async function async1() {
  await async2()
  console.log('async1 end')
}
async function async2() {
  console.log('async2 end')
}
async1()

setTimeout(function() {
  console.log('setTimeout')
}, 0)

new Promise(resolve => {
  console.log('Promise')
  resolve()
})
  .then(function() {
    console.log('promise1')
  })
  .then(function() {
    console.log('promise2')
  })

console.log('script end')
```