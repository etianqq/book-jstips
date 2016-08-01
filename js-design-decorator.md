# 装饰器模式

向预定义对象中添加功能，从而在运行时可以调整对象。

实现方式：
1. 原型链

        function Sale(price) {
            this.price = price || 100;
        }
        Sale.prototype.getPrice = function () {
            return this.price;
        };
        Sale.prototype.decorate = function(decorate){
            var F = function(){}, overrides = this.constructor.decorators[decorate], i,newobj;
            F.prototype = this;
            newobj = new F();
            newobj.uber = F.prototype;
            for(i in overrides){
                if (overrides.hasOwnProperty(i)){
                    newobj[i] = overrides[i];
                }
            }
            return newobj;
        };

        Sale.decorators = {};

        Sale.decorators.fedtax = {
            getPrice: function () {
                var price = this.uber.getPrice();
                price += price * 5 / 100;
                return price;
            }
        };

        Sale.decorators.quebec = {
            getPrice: function () {
                var price = this.uber.getPrice();
                price += price * 7.5 / 100;
                return price;
            }
        };

        Sale.decorators.money = {
            getPrice: function () {
                return '$' + this.uber.getPrice().toFixed(2);
            }
        };

        Sale.decorators.cdn = {
            getPrice: function () {
                return 'CDN$' + this.uber.getPrice().toFixed(2);
            }
        };

        var sale = new Sale(100);
        sale = sale.decorate('fedtax');
        sale = sale.decorate('quebec');
        sale = sale.decorate('money');
        console.log(sale.getPrice());


2. 列表（将前一个方法的结果传递到下一个方法里）


