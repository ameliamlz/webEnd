## 改变this指向

1. //call的实现 函数绑定新的对象

   //注意重写方法要写在函数原型上

   Function.prototype.mycall = function(context=window){

    context.fn = this;

    let args = [...arguments].slice(1)

    let res = context.fn(args);

    delete context.fn;

    return res;

   }

   

   let foo = {

    value:1

   }

   

   function test(name, age){

    console.log(name, age);

    console.log(this.value);

   }

   

   test('klkl', 12);

   test.mycall(foo)

   

2. Function.prototype.myapply = function(context = window){

    context.fn = this;

    //判断是否有第二个参数

     if(arguments[1]) {

     result = context.fn(...arguments[1])

     } else {

     result = context.fn()

    }

   

    return result;

   }

   

   let foo = {

    value:'11'

   }

   function bar(name){

    console.log(name);

    console.log(this.value);

   }

   

   bar.myapply(foo, ['mml']);

   

3. 