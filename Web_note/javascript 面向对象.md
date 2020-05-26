
javascript 没有类的概念
===
 * 可以把 ECMAScript 中的对象想象成散列表(对象名:值 组成的名值对),其中的值可以是数据/函数
   | 对象名 | 值 |
   -|-   
   | 对象名1 | 值1(Data/Function) |  

### 每个对象都是基于一个引用类型创建
  + 如创建一个对象(早期写法)
    ```js
      var person = new Object();
      person.name="Mike";
      person.age = 18;
      person.job = "Software Engineer";

      person.sayName = function(){
          alert(this.name);
      };
    ```  
  + 使用字面量语法修改成
    ```js
      var person = {
          name:"Mike",
          age : 18,
          job : "Software Engineer",
          sayName : function(){
            alert(this.name);
          }
      };
    ```