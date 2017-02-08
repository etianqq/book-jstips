#模块 Modules

每一个ES6模块都是一个包含JS代码的文件，模块本质上就是一段脚本，而不是用module关键字定义一个模块，但是模块与脚本还是有两点区别：

* 在ES6模块中，无论你是否加入“use strict;”语句，默认情况下模块都是在严格模式下运行。
* 在模块中你可以使用import和export关键字。

####基础知识

```
===>kittydar.js

export function detectCats(canvas, options) { .. }
export class Kittydar { ... 处理图片的几种方法 ... }
// 这个helper函数没有被export。
function resizeCanvas() {...}
...

===>demo.js
import {detectCats, Kittydar} from "kittydar.js";
...
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

####Default exports