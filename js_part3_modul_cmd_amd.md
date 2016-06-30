# 模块(cmd/amd)

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