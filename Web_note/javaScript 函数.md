
## javaScript 函数  

参考书籍
---
  + 《JavaScript高级程序设计》(第 3 版) 3.7 节 `函数`

3.8 小结 待读
---

###  函数的参数  
  + js 的函数参数可以是 js 中的任何数据类型
  + js 的函数接受的参数在内部是用一个数组来表示的
  + 即使你定义的函数只接受2 个参数，调用该函数时也可以改变参数个数:1 个、3 个或者无参
  + 在函数体内可以用 arguments 对象来访问参数数组，即获取每一个参数  
  + 函数定义后调用函数时命名参数若无传递值,形式如
    ```javascript 
    function func_name(para_a,para_b){
        console.log(para_b);
    }

    func_name(a);   // 输出 undefined
    ```
    一样，将被自动赋予 undefined 值，效果就像 ```var num;``` 。


#### `arguments`的特性
  + arguments 对象不是 Array 的实例，只是与数组类似  
  + 访问参数可用方括号语法 arguments[0]，即访问第一个参数，依此类推   
  + arguments 的值永远与对应命名参数的值同步  
  -例如-   
  ```javascript
    function demo_doAdd_arguments(num1,num2) {
        arguments[1] = 10;
        var addResult = arguments[0]+num2;
        console.log(addResult); 
    } 
  ```
  如若运行
  ```javascript
    demo_doAdd_arguments(1,2);  // 输出 11
  ```
  运算过程可理解为
  > 1. num1 == 1, num2 == 2;
  > 1. arguments[1] 也就是 num2 赋值 10
  > 1. 此时 num1 值为 1,num2 值为 10
  > 1. addResult 的值为 num1 + num2 == 11


### javascript 没有重载

  + 重载的概念在 C,java 等一些语言中，可以为一个函数(函数名相同)编写两个定义，只要两个函数接受参数的类型和数量不同即可。

  + 在javascript中定义了两个名字相同的函数，那么该名字只属于后定义的函数(*后定义的函数覆盖了先定义的函数*)


对 ECMAScript 的特性列举
---
  待续...