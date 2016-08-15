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
    
####CMD/AMD创建模块
    (function (root, factory) {

        "use strict";

        // CommonJS module is defined
        if (typeof module !== 'undefined' && module.exports) {
            module.exports = factory(require('jquery'), require('bootstrap'));
        }
        // AMD module is defined
        else if (typeof define === "function" && define.amd) {
            define("bootstrap-dialog", ["jquery", "bootstrap"], function ($) {
                return factory($);
            });
        } else {
            // planted over the root!
            root.BootstrapDialog = factory(root.jQuery);
        }
    }(this, function ($) {
        // your module codes
        return MyModel;
    })