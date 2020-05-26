# js 引用类型

### 1. Object 类型

1. 创建 Object 实例的两种形方式
    ```javascript
    // 方法 1 使用 new 操作符后跟 Object 构造函数
    var person = new Object();
    person.name = "Mike";
    person.age = 16;
    person.sex = "male";

    // 方法 2 “对象字面量表示法”
    var person={
        name:"Mike",
        age:16,
        sex:"male"
    };
    ```
    **注**
    > + 定义 person 每个属性间都需要用`,`隔开，最后一个属性之后不能加上`,`，否则 IE7 以及更早版本的 Opera 中导致错误
    
    属性名可以使用字符串

    ```javascript
    var person={
        name:"Mike",
        age:16,
        5:true
    };
    ```
    最后属性名类型为数值的 `5` 最后都会转化为字符串

    或者也可以将以上的方法 1 和方法 2 结合起来使用，不过就是看起来有些奇怪

    ```javascript
    var person = {};
    person.name = "Mike";
    person.age = 16;
    person.sex = "male";
    ```

1. 使用对象字面量法创建对象给一种封装数据的感觉，也是向函数传递大量可选参数的首选方式

    ```javascript
    function displayInfo(args) {

        var output = "";

        if (typeof args.name == "string") {
            output += "Name: " + args.name + "\n";
        }

        if (typeof args.age == "number") {
            output += "age: " + args.age + "\n";
        }

        if (typeof args.sex == "boolean") {

            output += "sex: ";

            if(args.sex == true){
                output += "male";
            }else{
                output += "female";
            }

            output +="\n";        
        }

    console.log(output);
    }

    // 测试函数
    displayInfo(
        {
            name:"Mike",
            age:15,
            sex:true
        }
    );

    displayInfo(
        {
            name:"Lucy",
            age:9,
            sex:false
        }
    );
    ```

1. 新建对象并存储属性值后就需要访问该对象的属性，可以用“点表示法”
    ```javascript
    console.log(person.name);
    ```  
    也可以用方括号`[]`法
    ```javascript
    console.log(person["name"]);
    ```

    **方括号法中的字符串也可以用变量来代替**
    ```javascript  
    var propertyName = "name";
    console.log(person[propertyName]);
    ```

1. 属性的命名是可以使用非数字非字母或者是关键字和保留字，如
    > person["first name"] = "Mike";   

    **如果使用点表示法来访问属性会语法错误，这个时候就要使用方括号表示法**

*注*
  + 除非必须使用变量来访问属性，<u>否则我们推荐使用点表示法</u>

### Array 类型

  + 使用 Array 的构造函数形如  
    ```js
      var persons = new Array(); // 使用 构造函数时，也可以省略 new 关键字
      var persons_num = new Array(num); // 已知元素数量的数组
    ```  

  + 使用数组字面量表示法，形如  
    ```js
      var colors = ['red','blue','green']; // 创建一个包含 3 个字符串的数组
      var name = []; // 创建空数组
    ```
#### 在 colors Array 对象创建之后，对其中的某个已知索引值(位置)的元素进行读取、修改、新增操作，如下  
     ```js  
       console.log(colors[0]); // 显示第一项
       colors[2] = "black"; // 修改第三项
       colors[3] = "brown"; // 新增第四项
       console.log(colors.length);
     ```  
    
   + 如若  
     ```js
      colors[99] = "gray"; // 新增第 100 项
      console.log(colors.length); // 输出新的数组长度 100
     ```  
     索引值已超出 colors 在初始化时的最大长度时，就会重新计算长度
    
    + 而输出没有赋值的第 5~99(即索引值为 4~98)项
     ```js
      for(var i =4;i<colors.length-1;i++){
          console.log(colors.length); // 输出
      }
      
     ```
    
#### 利用数组的转换方法操作 Array 类型对象(如输出整个数组)
   + 输出包含有效值元素的 Array
     ```js
       var colors = ["red","blue","green"];
       console.log("colors.'"+toString()+"'输出值:"+colors.toString());
       console.log("colors.'"+valueOf()+"'输出值:"+colors.valueOf());
       console.log("colors的输出值:"+colors);
     ```
   + 如果是使用 join 进行格式化输出，输入代码如
     ```js
       var colors = ["red","blue","green"];
       console.log(colors.join('|')); // 以“|” 隔开
       console.log(colors.join('、')); // 以 “、” 隔开
       console.log(colors.join()); // 无参数
       console.log(colors.join(undefined)); // 参数为 undefined
     ```
     **输出**
     ```
       red|blue|green
       red、blue、green
       red,blue,green
       red,blue,green
     ```
     *调用 array 类型对象的 join() 方法时传入参数为`无参数` 或 `undefined` 时，就会将每个元素都以 `,` 隔开*

#### 利用栈方法对操作 Array 类型对象(添加/删除元素)
   + 栈的特性 -- `后进先出(LIFO:'Last-In-First-Out')`
     
   + 栈的方法
     - 进/入 栈 `push` 向栈顶压入元素 
     - 出/退 栈 `pop` 取出栈顶元素
    
     ```js
       var array_num = ['first','second','third']; // 
       array_num.push('forth');  // 
       array_num.pop(); // 
     ```
     **array_num 元素的变化情况**
     ```
       初始化栈形式的数组：first,second,third
       array_num.push(forth)：first,second,third,forth
       array_num.pop()：first,second,third
     ```

#### 利用队列方法对操作 Array 类型对象(添加/删除元素)
   + 队列的特性 -- `先进先出(FIFO:'First-In-First-Out')`
     - 在列表的末端(队尾)添加项  

     - 在列表的前端(队首)删除项  

   + 队列的方法
     - 进/入 队列 `push` 元素从数组末端(队尾)进入  
       
     - 出/退 队列 `pop` 元素从数组顶端(队首)移出
       实现此操作的是 shift() 方法 -- 移除数组的第一个元素

     *使用 `shfit()`,`push()` 模拟队列元素出队、入队*
     ```js
       var array_num = ['first','second','third']; // 
       array_num.push('forth'); 
       array_num.shift();  // 
     ```
     **array_num 元素的变化情况**
     ```
       初始化队列结构的数组：first,second,third
       array_num.push(forth)：first,second,third,forth
       array_num.shift()：second,third,third
     ```
     - unshift() 与提取元素 shift() 相对
       可以加入任意参数来插入队列前端(队首) -- <b>也就是反方向入队</b>

      **使用 `unshfit()`,`pop()` 模拟队列元素反向地出队、入队**  
      ```js
       var array_num = ['first','second','third']; // 
       array_num.unshfit('forth'); 
       array_num.pop();  // 
      ```
     **array_num 元素的变化情况**
     ```
       初始化队列结构的数组：first,second,third
       array_num.push(forth)：forth,first,second,third
       array_num.shift()：forth,first,second
     ```
    
  *以上的`shfit()`和`push()`，`unshfit()`和`pop()`的队列示例即可组成双向队列的概念*

#### sort() 和 reverse()


#### concat() -- 

   + 创建目标数组的副本后在新数组上添加传递的参数，如果参数
     - 是数组，那么就会将数组的每一项都添加至结果
     - 不是数组，就会简单地将参数添加到结果数组的末尾  
   
      ```js
        var colors = ["red", "green", "blue"]; 
        var colors2 = colors.concat("yellow", ["black", "brown"]); 
        console.log(colors); // 输出 red,green,blue 
        console.log(colors2); // 输出 red,green,blue,yellow,black,brown
      ```  

#### slice() -- 