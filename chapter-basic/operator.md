# 8.操作符

|类别	|操作符	| 描述	|说明
| -- | -- |-- | -- |
|一元操作符	|++ /--	 |自增	|1、自增（减）有前置和后置两种类型，前置先自增（减）再参与其它运算，后置先参与其它运算再自增（减）。2、在ES中，自增（减）不仅适用于整数，它们可以作用于任意值，对于不是Number类型的值，会先按前一篇文章中的规则隐式转换为Number，然后再自增（减），此时变量类型也会变成Number类型。|
|按位操作符	|~	 |按位非	|按位取反，也即返回反码|
||&	 |按位与|	按位对齐，逐位操作，只有两个操作位均为1才返回1，否则该位返回0，最后将所有位操作结果组合返回|
||\	| 按位或|	按位对齐，逐位操作，只有两个操作位均为0才返回0，否则该位返回1，最后将所有位操作结果组合返回 |
||^	| 按位异或|	按位对齐，逐位操作，两个操作位不相同时返回1，否则该位返回0，最后将所有位操作结果组合返回|
||<<	 |左移|	二进制数向左移位，左移不会改变符号位 |
||>>|	 有符号右移	|二进制数向右移位，高位以符合位填充 |
||>>>|	 无符号右移	|二进制数向右移位，直接右移，对于正数，结果和>>相同，对于负数，会把负数的二进制补码当成正数的二进制码处理|
|其它操作符|()|	 分组操作符	|主要用途：1、结合逗号操作符用于赋值。例如：var num = (5,1,4,8,0);这里num最后的值为0。2、转换为表达式。比如``eval('('+jsStr+')');`` ``(function(){}());``又比如：3、用于调用函数。比如fn();|
||typeof|	 类型操作符	|返回一个字符串值：Undefined类型—>'undefined'、Null类型—>'object'、Boolean类型—>'boolean'、Number类型—>‘number'、String—>'string'、内置Function对象的实例—>'function'、其它Object类型—>'object'。（有些浏览器实现略有不同）|

####'&&','||' and '!'

1. Logical AND (&&)	
   
   ```expr1 && expr2```
   
   Returns expr1 if it can be converted to false; otherwise, returns expr2. Thus, when used with Boolean values, && returns true if both operands can be converted to true; otherwise, returns false.
   
   eg: 0&&1--->0, 1&&2--->2, 1&&true--->false
   
2. Logical OR (||)	
 
    ```expr1 || expr2```	
    
    Returns expr1 if it can be converted to true; otherwise, returns expr2. Thus, when used with Boolean values, || returns true if either operand can be converted to true; if both can be converted to false, returns false.
    
    1||2--->1, 0||3--->3, 4||true--->4, 0||true--->true
    
3. Logical NOT (!)

    ```!expr```
    
    Returns false if its single operand can be converted to true; otherwise, returns true.|
    
