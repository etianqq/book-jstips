#ESLint

官网：[http://eslint.cn/](http://eslint.cn/)

ESLint 是在 ECMAScript/JavaScript 代码中识别和报告模式匹配的工具，它的目标是保证代码的一致性和避免错误。在许多方面，它和 JSLint、JSHint 相似，除了少数的例外：

* ESLint 使用 Espree 解析 JavaScript。
* ESLint 使用 AST 去分析代码中的模式
* ESLint 是完全插件化的。每一个规则都是一个插件并且你可以在运行时添加更多的规则。

####使用

1. 安装: ```npm install -g eslint```
2. 新建一个配置文件: ```eslint --init```
3. ESLint 检测 JavaScript 文件: ```eslint test.js test2.js```
4. ESLint自动修复代码:```eslint test.js --fix```


