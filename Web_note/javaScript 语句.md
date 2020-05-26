
参考书籍
===
+ 《JavaScript高级程序设计》(第3版) 3.6节 `语句`

## javaScript 语句
   + for-in 语句
   + label 语句
   + with 语句
   + switch 语句
   + return 语句  


### for-in 语句  

  精准的迭代语句，可以用来枚举对象的属性   
  ```js  
    for(var property in expression){  
        statement;  
    }
  ```
+ property 属性  
+ expression 对象  
+ statement [网络释义] 语句  

**语句执行的逻辑解释**  
每次循环时，将 expression 中的存在的一个属性赋值给变量 properity,直到对象中的所有属性都被枚举了一遍。

*注*
+ *在使用 for-in 语句前先检测确认该对象的值不是 null/undefined*  

+ *循环条件中的 var 作用是让 properity 成为循环中的一个局部变量，如若不使用 var，虽然无语法错误，但是变量 properity 将上升为全局变量*


### label 语句

与 `break` 或 `continue` 配合使用
 
 + 在循环中与 `break` :

 ```js
    var num = 0;

    // 此处的 outermost 可以理解为嵌套循环语句块的命名
    outermost:          
    for (var i = 0; i < 10; i++) {
        for (var j = 0; j < 10; j++) {
            if (i == 5 && j == 5) {
                break outermost;
            }
            num++;
        }
    }

    console.log(num);     // 55
    // 以上的循环过程可以看成是一个运算过程变量值的变化
    // i == 0,j == 0, num == 1;
    // i == 0,j == 1, num == 2;
    // i == 0,j == 2, num == 3;
    // ...
    // i == 5,j == 4, num == 55;
    // i == 5,j == 5, 跳出 outermost 代码块;
    // 输出 num == 55
    // 程序结束
 ```

 + 在循环中与 `continue` :  
 ```javascript
    var num = 0;

    // 此处的 outermost 可以理解为嵌套循环语句块的命名
    outermost:          
    for (var i = 0; i < 10; i++) {
        for (var j = 0; j < 10; j++) {
            if (i == 5 && j == 5) {
                continue outermost;
            }
            num++;
        }
    }

    console.log(num);     // 95
    // 以上的循环过程可以看成是一个运算过程变量值的变化
    // i == 0,j == 0, num == 1;
    // i == 0,j == 1, num == 2;
    // i == 0,j == 2, num == 3;
    // ...
    // i == 5,j == 4, num == 55;
    // i == 5,j == 5, 并未跳出 outermost 代码块，只是跳出内循环，但是还是会执行外循环;
    // i == 5 时，j == 5/6/7/8/9 时的 num 并未执行 ++ 环节,所以 num 又原来会执行 100 次加 1 操作减少为加 95 次操作
    // i == 6,j == 0; num == 56;
    // ...  
    // i == 9,j == 9, num == 95;
    // 输出 num == 95
    // 程序结束
 ```
  
*如果使用 label 语句一定要使用描述性的标签，不要嵌套过多的循环*
  
### with 语句

*注意：<u>严格模式下不可使用 with 语句</u>*


形式如  
```
with ( expression ) statement;
```  
*目的主要是为了简化多次编写同一个对象的工作，例如*

```javascript
 var qs = location.search.substring(1); 
 var hostName = location.hostname; 
 var url = location.href; 
```  

上面几行代码都包含 location 对象，改写成 with 语句的形式为

```javascript
 with(location){ 
    var qs = search.substring(1); 
    var hostName = hostname; 
    var url = href; S
 } 
```  
*语义解释：以上每一个变量将会被认为是局部变量，with语句关联了 loaction 对象，如果在局部环境中找不到相关定义，就会在 location 中寻找是否有同名属性，有则使用该属性的值作为变量的值*


**大量使用`with`语句会降低性能，开发大型应用时，不建议使用。**

### switch 语句  

   + 需要混合多个情形：

   ```javascript
    switch(i){
        case 25:
        case 35: 
        /*合并两种情形*/
            console.log("25 or 35");
        default:
            console.log("Other");

    }
   ```

   + 在 ECMAScript 中，switch 语句中可以使用任何数据类型(无论是字符串 OR 对象)   

   + switch 语句在比较值时使用的时全等操作符`===`，因此不会发生类型转换符(比如数字 10 不等于字符串 "10")


### return 语句  

  + return 语句可以不带有任何返回值
  + 当无返回值时函数停止后返回`undefined`  

  **适用场景**

*严格模式对函数的限制*  

  + 不能把 函数/参数 命名为 eval 或 arguments;  
  + 同个函数内几个参数之间不能同名  

*否则代码将无法执行(因为 js 的执行是解释型执行过程，而非 C/C++ 等语言的先编译后运行)*
