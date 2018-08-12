# js-call-apply
call 和 apply 


ECMAScript规范为所有函数都包含两个方法(这两个方法非继承而来), call 和 apply 。
这两个函数都是在特定的作用域中调用函数,能改变函数的作用域，实际上是改变函数体内 this 的值 



    function test(x,y){
    return x*y;
    }
 
  这两个方法的参数不同 ，但作用是一样的
     function f(c,n){
          return test.call(this,a)
     }
        console.log(f(2,8)) //16

    function g(v,n){
        return test.apply(this,arguments)
    }

     console.log(g(8,9))  //72
     
     

    改变函数作用域
    
        var name = '小白';
        var obj = {name:'小红'};

        function sayName() {
            return this.name;
        }

        console.log(sayName.call(this));    //输出小白

        console.log(sayName. call(obj));    //输入小红


     
     
