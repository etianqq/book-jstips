# 模块
如何用JS实现类似requireJs的模块化？下面是个很精彩的例子：

    var MyModules = (function () {
        var modules = {};
        function define(name, deps, impl) {
            for (var i = 0; i < deps.length; i++) {
                deps[i] = modules[deps[i]];
            }
            modules[name] = impl.apply(impl, deps);  // module[name] is object
        }

        function get(name) {
            return modules[name];
        }

        return {
            define: define,
            get: get
        }
    }());

    MyModules.define("bar", [], function () {
        function hello(who) {
            return "let me introduce " + who;
        }
        return {
            hello: hello
        }
    });

    MyModules.define("foo", ["bar"], function () {
        var hungry = "hippo";
        var bar = arguments[0];

        function awesome() {
            console.log(bar.hello(hungry).toUpperCase());
        }
        return {
            awesome: awesome
        }
    });

    var foo = MyModules.get('foo');
    foo.awesome();