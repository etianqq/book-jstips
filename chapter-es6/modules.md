#模块 Modules

每一个ES6模块都是一个包含JS代码的文件，模块本质上就是一段脚本，而不是用module关键字定义一个模块，但是模块与脚本还是有两点区别：

* 在ES6模块中，无论你是否加入“use strict;”语句，默认情况下模块都是在严格模式下运行。
* 在模块中你可以使用import和export关键字。

####import
**import是ES6的加载机制，这种加载称为“编译时加载”或者静态加载**，即ES6可以在编译时就完成模块加载，效率要比 CommonJS模块的require加载方式高。

注意：**require加载称为“运行时加载”**，只有运行时才能得到这个对象。

ES6模块的设计思想，是尽量的静态化，使得编译时就能确定模块的依赖关系。import的加载机制使得静态分析成为可能，例如类型检验什么的，所以在支持ES6的语法情况下，建议用import。

####exports

```
function cube(x) {
  return x * x * x;
}
const foo = Math.PI + Math.SQRT2;
export { cube, foo };
--------------------------------------------
import { cube, foo } from 'my-module';
console.log(cube(3)); // 27
console.log(foo);    // 4.555806215962888
```
####Default exports

默认导出，只能导出一个函数、一个类、一个对象字面量...

```
export default function cube(x) {
return x * x * x;
}
-----------------------------------
import cube from 'my-module';
console.log(cube(3)); // 27
```
####重命名import和export
有时候，导出的名称会与你需要使用的其它名称产生冲突，ES6提供了重命名:
```
// 这两个模块都会导出以`flip`命名的东西。
// 要同时导入两者，我们至少要将其中一个的名称改掉。
import {flip as flipOmelet} from "eggs.js";
import {flip as flipHouse} from "real-estate.js";
```

在导出的时候也可以重命名:
```
function v1() { ... }
function v2() { ... }

export {
   v1 as streamV1,
   v2 as streamV2,
   v2 as streamLatestVersion
};
```
[
参考文章：mozilla exports](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/export)

#### ES 模块化为什么要设计成静态的?

一个明显的优势是：**通过静态分析，我们能够分析出导入的依赖。如果导入的模块没有被使用，我们便可以通过 tree shaking等手段减少代码体积，进而提升运行性能。**这就是基于 ESM 实现 tree shaking 的基础。

这么说可能过于笼统，我们从设计的角度分析这两种规范哲学的利弊。静态性需要规范去强制保证，不像 CommonJS 那样灵活，ES 模块化的静态性带来了限制：

  * 只能在文件顶部 import 依赖
  * export 导出的变量类型严格限制
  * 变量不允许被重新绑定，import 的模块名只能是字符串常量，即不可以动态确定依赖

这样的限制在语言层面带来的便利之一是：我们可以通过作用域分析，分析出代码里变量所属的作用域以及它们之间的引用关系，进而可以推导出变量和导入依赖变量的引用关系，在没有明显引用时，就可以进行去冗余。



