

**注**  
+ 以下的概念理解为个人结合教材和代码运行结果进行理解，仅供参考


### 基本类型 的值和 引用类型 的值  
 
* 基本类型的值 —— 简单的 **数据段** (<u>可以理解为简单的变量</u>)  

* 引用类型的值 —— 可能由多个值构成的 `对象`  

> 当复制保存着对象的某个变量时，操作的是对象的引用。
> 但在为对象添加属性时，操作的是实际的对象

如
  ```javascript
   var num1 = 19;
   var num2 = num1; // 19
   num1 = 15;
   console.log(num2); // 19
  ```
*此时 `num1`中的值 19 和 `num2` 中的值 19 是相互完全独立的两个个体*

而
  ```javascript
   var obj1 = new Object();// obj1 的值是指向一个存储在堆中的对象的指针
   var obj2 = obj1; // obj2 的值是指向 obj1 的值指向对象的指针
   obj2.age = 15;// 为 obj2 指向的对象添加属性 age,并赋值 15
   console.log(obj1.age); // 访问 obj1 的值所指向的对象的 age 属性 15
  ```
*因为 `obj1` 和 `obj2` 所指向的堆中同一个对象，那么在对 `obj2` 所指向的对象进行添加属性操作并赋值的时候，也就是操作实际的对象（如上文所示）*

### 动态的属性

如 
  ```javascript
   var person = "Mike";
   person.age = 19;
   console.log(person.age);   //Undefined
  ```
运行语句后，无语法错误，但是输出为 `undefined`
在给 person 变量定义了 age 属性后再访问属性时已然不见

而当
  ```javascript
   var person = new Object();
   person.name = "Mike";
   console.log(person.name);  //"Mike"
  ```
运行语句之后，输出的即为 `Mike`  
在给 person 变量定义了 name 属性后再访问属性依旧存在且值为 'Mike'.

**说明**
> + 只能给引用类型值动态地添加属性
> + 给引用类型的值添加属性后，只要该对象不被销毁或者该属性不被删除，那么这个属性将一直存在

### 传递参数——<small>按值传递</small>

> 按照 ECMAScript 的概念 —— 所有函数的参数都是<u>按值传递</u> 的。

 **注**
  <u>按值传递</u> ——将函数外部的值复制给函数内部的参数，如下 
1. 利用函数对 变量 进行赋值操作  

   ```javascript
   function addNum(num){
       num++;
       return num;
   }

   var inputNum = 5;
   var result  = addNum(inputNum);
   // inputNum == 5;
   // result == 6;
   ```
   **说明**
   在调用 addNum 函数的过程中 `inputNum` 作为参数，它的值被复制给了变量 `num` (按值传递)，而 `num` 的值再怎么变化也不会影响到函数外的 `inputNum` 的值  


1. 利用函数对 对象 进行赋值操作

   ```javascript
   function setName(obj) { 
       obj.name = "Mike";
   }

   var person = new Object(); //(1)
   setName(person); //(2)
   console.log(person.name); //(3)"Mike"
   ```
   **说明**
   (1) 创建一个对象，并将其保存在刚声明的 person 变量中  

   (2) 调用 setName 函数时，将变量 person 复制给 obj(上文提过，在对引用类型值进行复制时，实际上是复制出一个指向同一个对象的指针)，person 和 obj 引用的就是同一个对象，给 obj 所指向的对象添加一个属性 name 并赋值 "Mike";  

   (3) 输出变量 person 所引用的对象的 name 属性值为 "Mike"  

**以上的例 2 却不能证明函数参数的按值传递性，反而成为了 “按引用传递”的佐证命题，下面对示例进行修改**  

3. 利用函数对 对象 进行赋值操作(修订版)
   ```javascript
   function setName(obj) { 
       obj.name = "Mike";
       obj = new Object();
       obj.name = "Andy";
   }

   var person = new Object(); //(1)
   setName(person); //(2)
   console.log(person.name); //(3)"Mike"
   ```
   **说明**
   (1) 创建一个对象，并将其保存在刚声明的 person 变量中  

   (2) 调用 setName 函数，将变量 person 值复制给 obj，给 obj 所指向的对象添加一个属性 name 并赋值 "Mike";<u>创建一个新的对象并将其保存在 obj 中，对 obj 的值指向的对象给出一个新属性 name ，并赋值 "Andy"，退出函数</u>  

   (3) 输出变量 person 所引用的对象的 name 属性值为 "Mike"  

   *此时如果输出 `obj.name` 将得到值 "Andy"*

以上的例子就可以证明函数的作用对象无论是 基本类型值(变量)还是引用类型值(对象)，均是按照 <b>`按值传递`</b> 的原则  

### 检测类型

  + `typeof` 操作符
  + `instanceof` 操作符

#### `typeof` 

  + JavaScript 中有五大基本类型
    - Number
    - Boolean
    - NULL
    - String
    - Object

  使用 `typeof` 在变量值为null 或 Object 时都会返回 "Object",而检测引用类型的值时，`typeof` 的用处不大，只会返回"Object" <u>(规定所有的引用类型的值都是 Object 的实例)</u> ;如果想要知道引用类型的变量的具体什么类型，就可以使用  `instanceof` 操作符  
  ```javascript
  console.log(array instanceof Array);  //变量 array 是 Array ？
  console.log(obj instanceof Object);
  console.log(pattern instanceof RegExp);
  ```
  **说明**
  返回值为 true 则说明该表达式成立，且只要是引用类型值，`variable instanceof Object` 均成立;基本类型值不是对象，所以在使用 `instanceof` 操作符时始终返回 false;

  **额外**
  
