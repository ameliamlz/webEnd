## ES6

1. 新增symbol类型 表示独一无二的值，用来定义独一无二的对象属性名;

2. 变量的解构赋值(包含数组、对象、字符串、数字及布尔值,函数参数),剩余运算符(...rest);

5. 扩展运算符(数组、对象);

   对象：同名赋值/非同名赋值+{}；数组：占位符+[]; Object.assign()

   补充：对象遍历：getOwnPropertyNames()

6. 箭头函数;

5. Set和Map数据结构;

   区别：

   - set存储的值不能重复，map的值可重复
   - set的形式[value, value], map的形式{key, value}

9. Promise;

10. async函数：解决异步问题，函数是 `Generator` 函数的语法糖；语义化优势明显

11. Class;

9. Module语法(import/export)

10. Proxy/Reflect;

    new Proxy(target, handler): 监听更多的属性



###  let/const/var

- let/const

  1. let 会产生临时性死区，在当前的执行上下文中，会进行变量提升，但是未被初始化，所以在执行上下文执行阶段，执行代码如果还没有执行到变量赋值，就引用此变量就会报错，此变量未初始化。

  2. 重复声明报错

  3. 不绑定全局作用域

  4. let定义的值可修改； const声明不允许修改绑定，但允许修改值(对象)

     ps：日常开发尽量用const进行写保护， 能避免许多bug

- var

  函数作用域，变量的声明提升。以下两种情况无法删除var变量：
  
  - var声明的全局变量
  - var在函数范围内声明的局部变量
  
  

### ES6数组做了哪些扩展

- ...扩展运算符
- Array.from(): 将类数组对象和可遍历的对象转为真正的数组
-  Array.of()：将值转换为数组
- entries()，keys()，values()，find(), fill()



### 模板字符串/标签模板

在模板字符串中，空格、缩进、换行都会被保留， 支持嵌入变量，支持嵌套

遗留问题：如何处理用户输入？



### 箭头函数(和普通函数的区别)

1. 没有this，需通过查找作用域链来确定this指向
2. 没有arguments， 但可以访问外围的arguments
3. 不能用new
4. 不能用作迭代器
5. call/apply/bind不能改变this指向

自执行函数：

```
(function(){
    console.log(1)
})()
```

or

```
(function(){
    console.log(1)
}())
```



### ES6之迭代器和for of 

所谓迭代器，其实就是一个具有 next() 方法的对象，每次调用 next() 都会返回一个结果对象，该结果对象有两个属性，value 表示当前的值，done 表示遍历是否结束。

练习：用ES5语法实现迭代器

for of ： Symbol.iterator属性

ES6 为数组、Map、Set(键值相同) 集合内建了以下三种迭代器：entries()，keys()，values()



### Set数据结构

1. 本身是一个构造函数，可接受数组(或者具有可迭代属性的其他数据结构)作为参数

2. 操作方法：add(value)，delete(value)，has(value)，clear()

3. 遍历方法：keys()，values()，entries()，forEach()

   ```
   let set = new Set(['a', 'b', 'c']);
   console.log(set.keys()); // SetIterator {"a", "b", "c"}
   console.log([...set.keys()]); // ["a", "b", "c"]
   ```

4. 属性：

   - Set.prototype.constructor：构造函数，默认就是 Set 函数。
   - Set.prototype.size：返回 Set 实例的成员总数。

   小练习：模拟实现set



### WeakMap数据结构

1.  WeakMap 只接受对象作为键名

2. WeakMap 的键名所引用的对象是弱引用，容易被回收



















