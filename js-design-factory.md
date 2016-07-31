# 工厂模式

根据字符串指定的类型，在运行时创建对象。

      function CarMaker(){}

      CarMaker.prototype.drive = function(){
        return 'i have ' +  this.doors + ' doors!';
      }

      CarMaker.factory = function(type){
        var constr = type, newcar;
        if (typeof CarMaker[constr]!='function'){
          throw Error (constr + 'dose not exist!');
        }

        if (typeof CarMaker[constr].prototype.drive != 'function'){
          CarMaker[constr].prototype = new CarMaker();
        }

        newcar = new CarMaker[constr]();
        return newcar;
      }
      
      CarMaker.Compact = function(){
        this.doors = 4;
      }
      
      CarMaker.Convertible = function(){
        this.doors = 2;
      }
      
      CarMaker.SUV = function(){
        this.doors = 24;
      }
      
      // usage
      var corolla = CarMaker.factory('Compact');
      corolla.drive();