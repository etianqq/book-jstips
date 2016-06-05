# 类：面向对象编程

面向类的设计模式：实例化（instantiation）、继承（inheritance）和（相对）多态
（polymorphism）。

####寄生继承

    function Vehicle(){	
		this.engines = 1;
    }
    Vehicle.prototype.ignition = function(){
		console.log("Turning on my engine.");
    };
    Vehicle.prototype.drive = function(){	
		this.ignition();
		console.log("Steering and moving forward!");
    };
    //“寄生类” Car
    function Car(){
		var car = new Vehicle();
		car.wheels = 4;
		var vehDrive = car.drive;
		car.drive = function(){	
		vehDrive.call(this);	
		console.log("Rolling on all "+this.wheels+"wheels!");
		return car;	
    }
    var myCar = new Car();
    myCar.drive();
    // Turning on my engine!
    // Steering and moving forward!
    // Rolling on all 4 wheels!
    
    
####隐式混入
    var Something={	
		cool:function(){
			this.greeting="Hello World";
			this.count=this.count ? this.count+1 : 1;	
			}
    };
    Something.cool();	
    Something.greeting; //"Hello World"
    Something.count;	//1
    var Another={
		cool:function(){
                Something.cool.call(this);
			}
    };
    Another.cool();
    Another.greeting; // "Hello World"
    Another.count;	// 1 (count不是共享状态）