## new

//new 操作符重写

function myNew(ctor){

 let obj = {};

 //设置对象的原型

 if(ctor.prototype !== null){

  obj.__proto__ = ctor.prototype;

 }

 //改变this的指向

 let res = ctor.apply(obj, Array.prototype.slice.call(arguments, 1))

 //如何该函数没有返回对象， 则返回对象本身的引用

 if((typeof res === 'object' || typeof res === 'function')&& typeof res !== null){

  return res;

 }

 return obj;

}



let a = myNew(String, 1);