#作用域和作用域链

####1. 作用域（也称为执行上下文）
一句话简述**“作用域”**---“执行JavaScript代码时，JavaScript引擎会创建一个执行上下文，它设定了代码执行时所处的环境”。


当页面加载完：

1. 创建一个全局的执行上下文（this指向我们熟知的window）；
2. 每执行一个JavaScript函数，都会创建一个对应的执行上下文；
3. 函数里面可能执行嵌套函数......继续创建子函数的执行上下文；
4. 最终，会创建出一个栈，当前作用域在栈顶，全局作用域在栈底；



