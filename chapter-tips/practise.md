# 练习题

第一题
 
    console.log(a);
    var a = 3;    // undefined
    -----------------------
    console.log(a);
    a = 3;    // throw ReferenceError

第二题

    foo();	// TypeError
    bar();	// ReferenceError
    var foo=function bar()	{...}

第三题

    for (var i = 0; i < 10; i++) {  
        setTimeout(function () {
        alert('I am link #' + i);
      }, 100);
    }


