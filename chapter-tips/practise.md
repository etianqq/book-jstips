# 练习题

#### 第1题
 
    console.log(a);
    var a = 3;    // undefined
    -----------------------
    console.log(a);
    a = 3;    // throw ReferenceError

#### 第2题

    foo();	// TypeError
    bar();	// ReferenceError
    var foo=function bar()	{...}

#### 第3题

    for (var i = 0; i < 10; i++) {  
        setTimeout(function () {
        alert('I am link #' + i);
      }, 100);
    }

#### 第4题

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
