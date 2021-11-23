## 改变this指向-call-apply-bind

1. call的实现 函数绑定新的对象

   ```
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
   ```

2. apply实现

    ```javascript
    Function.prototype.myapply = function(context = window){
       context.fn = this;
       //判断是否有第二个参数
       if(arguments[1]) {
       	   result = context.fn(...arguments[1])
       }else{
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
    
    ```

3. bind实现(存疑：value undefined？)

    ```
    Function.prototype.bind2 = function(content) {
      if(typeof this != "function") {
          throw Error("not a function")
      }
      // 若没问参数类型则从这开始写
      let fn = this;
      let args = [...arguments].slice(1);
      
      let resFn = function() {
          console.log(this instanceof resFn)
          return fn.apply(this instanceof resFn ? this : content,args.concat(...arguments) )
      }
      function tmp() {}
      tmp.prototype = this.prototype;
      resFn.prototype = new tmp();
      
      return resFn;
    }
    var foo = {
      value: 1
    };
    
    function bar(name, age) {
      this.habit = 'shopping';
      console.log(this.value);
      console.log(name);
      console.log(age);
    }
    
    var bindFoo = bar.bind2(foo, 'daisy');
    
    var obj = new bindFoo('18');
    
    ```

    

