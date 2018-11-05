# js-call-apply
call 和 apply 


  call()
   
      function Person(name,age,sex){
         this.name=name;
         this.age=age;
         this.sex=sex;
      }

    function Student(name,age,sex,tel,color){
     //  下面new Student后就在这里形成了   var this={} 
      Person.call(this,name,age,sex)   //call 调用别人的方法或者属性 完成自己的功能
    //这里用call 调用 Person()方法的属性，完成自己功能
    // Person.call(this,name,age,sex)之后相当于在这里写上了 this.name=name;this.age=age;this.sex=sex;
         this.tel=tel;
         this.color=color;
      }

     var student=new Student("张三",22,"男",138,"red")
    //张三-22-男-138-red
    console.log(student.name+"-"+student.age+"-"+student.sex+"-"+student.tel+"-"+student.color)



ECMAScript规范为所有函数都包含两个方法(这两个方法非继承而来), call 和 apply 。
这两个函数都是在特定的作用域中调用函数,能改变函数的作用域，实际上是改变函数体内 this 的值 

      /*apply()方法*/
    function.apply(thisObj[, argArray])

    /*call()方法*/
     function.call(thisObj[, arg1[, arg2[, [,...argN]]]]);
     
 它们各自的定义：

        apply：调用一个对象的一个方法，用另一个对象替换当前对象。例如：B.apply(A, arguments);即A对象应用B对象的方法。

        call：调用一个对象的一个方法，用另一个对象替换当前对象。例如：B.call(A, args1,args2);即A对象调用B对象的方法。
        
        实际上，apply和call的功能是一样的，只是传入的参数列表形式不同。


       示例代码：

    （1）基本用法

     改变函数作用域

           function add(a,b){
              return a+b;  
            }
            function sub(a,b){
              return a-b;  
            }
            var a1 = add.apply(sub,[4,2]);　　//sub调用add的方法
            var a2 = sub.apply(add,[4,2]);
            alert(a1);  //6     
            alert(a2);  //2

            /*call的用法*/
            var a1 = add.call(sub,4,2);
            
        （2）实现继承 
            
            function Animal(name){
              this.name = name;
              this.showName = function(){
                    alert(this.name);    
                }    
            }

            function Cat(name){
              Animal.apply(this,[name]);    
            }

            var cat = new Cat("咕咕");
            cat.showName();  //咕咕

            /*call的用法*/
            Animal.call(this,name);     
            
        （3）多重继承   
            
             function Class10(){
              this.showSub = function(a,b){
                    alert(a - b);
                }   
            }

            function Class11(){
              this.showAdd = function(a,b){
                    alert(a + b);
                }  
            }

            function Class12(){
              Class10.apply(this);
              Class11.apply(this);   
              // Class10.call(this);
              //Class11.call(this);  
            }

            var c2 = new Class12();
            c2.showSub(3,1);    //2
            c2.showAdd(3,1);    //4
            
            
     
     
