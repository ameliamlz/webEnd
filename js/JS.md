## 其它

1. ASI:在一些关键字后面自动插入分号，如return
2. delete



### 待解决

Array.prototype.push.call()等类似写法



### JS的了解

基于原型的动态语言，主要独特特性有this，原型链。分为**语言标准**(ES6)和**宿主环境**(浏览器：DOM+BOM)



## 引入脚本的方式

1. 通过<script>标签静态引入

2. 动态加载脚本

   会影响资源的优先级，降低性能，可link提前声明资源

   ```dart
   var scriptElement=document.createElement("script");
   scriptElement.src="js/test.js";
   (document.getElementsByTagName("head")[0] || document.body).appendChild(scriptElement);
   ```

3. <script defer>:只针对外部js文件，异步加载,延迟执行，执行顺序一致

4. <script async>:只针对外部文件，异步加载，立即执行，执行顺序不定



## 变量

变量和函数声明(和函数表达式做一个区分)会被提升。

### var

以下两种情况无法删除var变量：

- var声明的全局变量
- var在函数范围内声明的局部变量



### for in 和 for of

- for-in得到对象的key或数组、字符串的下标。 
- for-of得到对象的value或数组、字符串的值，另外还可以用于遍历Map和Set。



### 数据类型

- 基本类型：Boolean/Number/String/Undefined/Null/Symbol/Bigint，存放在栈内存中的简单数据段，数据大小确定，内存空间大小可以分配。

  注：

  1. Bigint(创建大数，在末尾加个n)，不支持一元加号运算符，不允许和Number进行混合操作，0n为false，其他的值都为true，可以进行sort，可以进行位运算

  2. symbol设置独一无二的变量。利用 `symbol` 不会被常规的方法（除了 Object.getOwnPropertySymbols外）遍历到，所以可以用来模拟私有变量。（可继续补充）

     Symbol.hasInstance：ES6内部重写了instanceof
     
     Symbol.iterator接口
     
     Symbol.toPrimitive：类型转换时会用到
     
     

- 引用类型：Object 对象子类型(Function/Array/RegExp/Date/Math)，**引用(指针)存放在栈区，实际对象保存在堆区**，每个空间大小不一样，要根据情况开进行特定的分配。当我们需要访问引用类型（如**对象，数组，函数**等）的值时，首先从栈中获得该对象的地址指针，然后再从堆内存中取得所需的数据。



## Object.defineProperty()的用法

直接在一个对象上定义一个新属性，或者修改一个对象的现有属性，并返回此对象。



## 0.1+0.2 !== 0.3 经典题的背后

ECMAScript 采用 IEEE754 标准，全称 IEEE 二进制浮点数算术标准。在 IEEE754 中，规定了四种表示浮点数值的方式：单精确度（32位）、双精确度（64位）、延伸单精确度、与延伸双精确度。ES中使用的是双精度。

0.1和0.2转换成二进制时变成无限循环小数，保存成浮点数一定会产生的问题

- 第0位：符号位，0表示正数，1表示负数(s)
- 第1位到第11位：储存指数部分（e）
- 第12位到第63位：储存小数部分（即有效数字）f。**Number.MAX_SAFE_INTEGER == Math.pow(2,53) - 1**，有效数字指小数点前始终有一位，所以默认省略 53=52+1，超过精度时会丢失精度。（Number的存储空间）

![img](https://p1-jj.byteimg.com/tos-cn-i-t2oaga2asx/gold-user-assets/2018/9/16/165e0eb7f4d6c50f~tplv-t2oaga2asx-watermark.awebp)



### settimeout设置为0时会怎样？

settimeout会有一个时间的最小值，是几毫秒，当你设置0的时候是不会成功的

事件循环



### JS三种加载方式的区别

onload：加载完成后再执行(否则可能监听不到)

- 正常模式：加载时会阻塞浏览器

- 延缓模式：异步加载，推迟执行，具体时会等到DOMContentLoaded事件即将被触发时

- 异步模式：异步加载，加载完成后会立即执行JS脚本

  

### js之参数传递

值传递/引用传递/共享传递

在函数传参的时候传递的是对象在堆中的内存地址值，注意哪些操作是分配了新的空间地址



### typeof & instanceof & constructor & Object.prototype.toString 

- typeof 主要用来判断数据类型，返回结果包括：number、string、boolean、undefined、object、function。typeof null is object & typeof NaN === 'number'，对于基本数据类型除null之外都能显示正常的类型，对于引用类型，都显示位object。

  **原理**：js底层存储变量：

  1. 000：对象
  2. 010：浮点数
  3. 100：字符串
  4. 110：布尔类型
  5. 1：整数
  6. null：所有机器码均为0
  7. undefined：用-2^30整数表示

- instanceof 用于判断对象是谁的实例，主要的实现原理就是只要右边变量的 `prototype` 在左边变量的原型链上即可。注意下图中 Function和Object复杂关系。

  ![img](https://p1-jj.byteimg.com/tos-cn-i-t2oaga2asx/gold-user-assets/2018/5/28/163a55d5d35b866d~tplv-t2oaga2asx-watermark.awebp)

- constructor: 某个实例对象时哪一个构造函数产生的（重写原型后此属性会丢失，因此不可信）

- Object.prototype.toString  比较全面

小练习：实现instanceof（getPrototypeOf）

### null & undefined

null表示空对象 undefined 表示已在作用域中但未赋值的变量

灵魂拷问：null是对象吗？

深思熟虑：这是js的一个bug，typeof null === object，这是因为在js中以000开头的代表是对象，而null的表示是全0， 所以将它误判为object



### 类型转换

注：JS中类型转换只有三种类型的转换

- 转换为Number类型：Number()，parseInt()，parseFloat()
- 转换为String类型：String()，toString()
- 转换为Boolean类型： Boolean()

1. 转换为boolean

   **除了“+-0/NaN/空字符串/null/undefined”五个值是false，其余都是true**

   - 显示：Boolean()
   - 隐式：逻辑判断/逻辑运算符

2. 转换为String

   - 显示：String()  特殊:+-0都转为0 eg. String([1,2,3])    //"1,2,3"  || String({})    //"[object Object]"

   - 隐式："+" 操作符，且有一个操作数为字符串/一个操作数是对象

     JavaScript 对象有两个不同的方法来执行转换，一个是 `toString`，一个是 `valueOf`

     所有的对象除了 null 和 undefined 之外的任何值都具有 `toString` 方法。

     小规则：

     - 数组的 toString 方法将每个数组元素转换成一个字符串，并在元素之间添加逗号后合并成结果字符串。

     - 函数的 toString 方法返回源代码字符串。

     - 日期的 toString 方法返回一个可读的日期和时间字符串。

     - RegExp 的 toString 方法返回一个表示正则表达式直接量的字符串

       ```
       console.log(({}).toString()) // [object Object]
       
       console.log([].toString()) // ""
       console.log([0].toString()) // 0
       console.log([1, 2, 3].toString()) // 1,2,3
       
       // function (){var a = 1;} 源码字符串
       console.log((function(){var a = 1;}).toString())
       
       console.log((/\d+/g).toString()) // /\d+/g
       
       // Fri Jan 01 2010 00:00:00 GMT+0800 (CST) 日期字符串
       console.log((new Date(2010, 0, 1)).toString()) 
       //用valueof将对象转成字符串
       var date = new Date(2017, 4, 21);
       console.log(date.valueOf()) // 1495296000000
       ```

3. 转换为Number

   - 显示：Number()

     1. 字符串转换为数字：空字符串变为0，如果出现任何一个非有效数字字符，结果都是NaN

        ```
        console.log(Number("123")) // 123
        console.log(Number("-123")) // -123
        console.log(Number("1.2")) // 1.2
        console.log(Number("000123")) // 123
        console.log(Number("-000123")) // -123 忽略了里面的0
        console.log(Number("0x11")) // 17
        console.log(Number("")) // 0
        console.log(Number(" ")) // 0？
        console.log(Number("123 123")) // NaN
        ```

     2. 布尔转换为数字：1/0

     3. null和undefined转换成数字：null为 0，undefined为NaN

     4. Symbol转数字：会报错

     5. BigInt转数字：去除'n'

     6. 对象转换为数字

        - 先调用对象的 `Symbol.toPrimitive` 这个方法，如果不存在这个方法
        - 再调用对象的 `valueOf` 获取原始值，如果获取的值不是原始值
        - 再调用对象的 `toString` 把其变为字符串
        - 最后再把字符串基于`Number()`方法转换为数字

   - 隐式：

     1. 比较操作：>，<，>=，<=
     2. 按位操作：| & ^ ~
     3. 算数操作：+ - * / (注意上面+号的特殊情况)
     4. 一元+操作

4. 操作符==两边的隐式转换规则

   注：== 和=== 的区别：允许强制类型转换/不允许；值相等即可 / 值和类型都要相等；

   - 对象==字符串：将对象转换为字符串
   - 对象==对象：比较的是堆内存地址，地址相同则相等

5. null == undefined

6. 原始值转对象

   通过调用构造函数

9. 布尔值和数字无论加减，都将布尔值转为数字

8. 字符串和数字比较：字符串转数字

9. 其他类型和布尔类型：先把布尔类型转数字

10. 对象和非对象比较：执行对象的ToPrimitive()

## 类型转换的问题

​	引例：[] == ![]结果是什么？为什么？

6. JSON.stringify

   - 处理基本类型时，与使用toString基本相同，结果都是字符串，除了 undefined

   - 布尔值、数字、字符串的包装对象在序列化过程中会自动转换成对应的原始值

     ```
     JSON.stringify([new Number(1), new String("false"), new Boolean(false)]); // "[1,"false",false]"
     ```

   - undefined、任意的函数以及 symbol 值，在序列化过程中会被忽略（出现在非数组对象的属性值中时）或者被转换成 null（出现在数组中时）

   - JSON.stringify 有第二个参数 replacer，它可以是数组或者函数，用来指定对象序列化过程中哪些属性应该被处理，哪些应该被排除

   - 如果一个被序列化的对象拥有 toJSON 方法，那么该 toJSON 方法就会覆盖该对象默认的序列化行为：不是那个对象被序列化，而是调用 toJSON 方法后的返回值会被序列化

     ```
     var obj = {
       foo: 'foo',
       toJSON: function () {
         return 'bar';
       }
     };
     JSON.stringify(obj);      // '"bar"'
     JSON.stringify({x: obj}); // '{"x":"bar"}'
     ```
   
   
   

### RegExp基本用法

1. 获取匹配：pattern.exec(text)，返回匹配的字符
2. 是否模式匹配：pattern.test(text)，返回true/false



### Object.is 和 === 的区别

0===0，但如果0为分母就要区分正负0了；NaN不等于它本身

```
+0 === -0;           // true
Object.is(+0, -0)    // false

NaN === NaN          // false
Object.is(NaN, NaN)  // true
```



### Map、weakMap和Set

set：数据不重复

map：允许多种数据类型的key

weakmap：只能以复杂数据类型作为key(如数组)，并且key值是弱引用



### 闭包

![image.png](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/c508a8bbade94a699d0baad47e5d43ed~tplv-k3u1fbpfcp-watermark.awebp)

闭包属于一种特殊的作用域，称为 **静态作用域**。它的定义可以理解为: **父函数被销毁** 的情况下，返回出的子函数的`[[scope]]`中仍然保留着父级的单变量对象和作用域链，因此可以继续访问到父级的变量对象，这样的函数称为闭包。

闭包是指有权访问另一个函数作用域中的变量的函数。当函数可以记住并访问所在的词法作用域时，就产生了闭包，即使函数是在当前词法作用域之外执行。（按上下文分析）

- 闭包用途：

  1. 能够访问函数定义时所在的词法作用域(阻止其被回收)
  2. 私有化变量
  3. 模拟块级作用域
  4. 创建模块

- 闭包带来的问题

  1. 经典问题：父级变量，所有闭包共享。

  2. 会导致函数的变量一直保存在内存中，过多的闭包可能会导致内存泄漏；

     解决闭包带来的内存问题：就是在退出函数之前，将不使用的局部变量全部删除。

- 闭包的表现形式

  1. 返回一个函数

  2. 作为函数参数传递

  3. 在定时器、事件监听、Ajax请求、跨窗口通信、Web Workers或者任何异步中，只要使用了回调函数，实际上就是在使用闭包。

  4. IIFE(立即执行函数表达式)创建闭包, 保存了`全局作用域window`和`当前函数的作用域`

     ```
     var a = 2; 
     (function IIFE(){  // 输出2*  
     	console.log(a); 
     })();
     ```



### 作用域

ES5 中只存在两种作用域：全局作用域和函数作用域。

ES6新增块级作用域。

- 非匿名自执行函数，外部or内部函数变量为 **只读** 状态，无法修改

### 词法(静态)作用域（js）和动态作用域（bash）

JavaScript 采用的是词法作用域，函数的作用域在函数定义的时候就决定了,而与词法作用域相对的是动态作用域，函数的作用域是在函数调用的时候才决定的。

ps：函数变量和普通变量



### 执行上下文(栈)-对象

概念：当**执行**到一个函数的时候，就会进行准备工作，这里的“准备工作”，叫做"执行上下文，注意栈的调用顺序

可执行代码(上下文)的类型：

- 全局执行上下文
- 函数执行上下文
- eval执行上下文

每个执行上下文包含：

- 变量对象(Variable object，VO)

- 作用域链(Scope chain)

- this（有些存疑）



### 原型到原型链

**原型:** 对象(除null)中固有的`__proto__`属性，该属性指向对象的`prototype`原型属性。

**原型链:** 当我们访问一个对象的属性时，如果这个对象内部不存在这个属性，那么它就会去它的原型对象里找这个属性，这个原型对象又会有自己的原型，于是就这样一直找下去，也就是原型链的概念。原型链的尽头一般来说都是`Object.prototype`所以这就是我们新建的对象为什么能够使用`toString()`等方法的原因。用`hasOwnProperty`来检验对象自身是否有这个属性，用`in`来检验原型链上是否包含此属性。

每个原型都有一个 constructor 属性指向关联的构造函数，每个函数都有一个 prototype 属性

```
Object.prototype.__proto__ === null
```

**特点:** `JavaScript`对象是通过引用来传递的，我们创建的每个新对象实体中并没有一份属于自己的原型副本。当我们修改原型时，与之相关的对象也会继承这一改变。

![img](https://raw.githubusercontent.com/mqyqingfeng/Blog/master/Images/prototype3.png)



### 事件监听的两种方式

- onclick
- addEventListener

### 事件循环(EventLoop)

![img](https://p1-jj.byteimg.com/tos-cn-i-t2oaga2asx/gold-user-assets/2019/1/18/1685f03d7f88792b~tplv-t2oaga2asx-watermark.awebp)

概念：JS是单线程的，为防止一个函数执行时间过长阻塞后面的代码，所以会将同步代码压入执行栈中，将异步代码推入任务队列，任务队列又分为宏任务和微任务队列，因为宏任务队列的执行时间比较长，所以微任务要优先于宏任务队列。每次单个宏任务执行完之后，就会清空微任务。微任务：promise/promise.then/process.nextTick()(Node中),宏任务：**Script**/setTimeout(时间结束后执行)/setInterval(间隔时间内不断执行)/setImmediate/I/O/UI rendering

优先级：

- setTimeout = setInterval 一个队列
- setTimeout > setImmediate 
- process.nextTick > Promise

### 事件流

事件流是指网页元素接收事件的顺序，包括三个阶段：事件捕获阶段、处于目标阶段、事件冒泡阶段。

- Dom0级

- Dom2级事件有三个参数：第一个参数是事件名（如click）；第二个参数是事件处理程序函数；第三个参数如果是true的话表示在捕获阶段调用，为false的话表示在冒泡阶段调用。

- Dom3级

  注：同一个元素的同一种事件只能绑定一个函数，否则后面的函数会覆盖之前的函数



### 事件冒泡、捕获（委托）

事件捕获发生在事件冒泡之前

**事件冒泡**指在在一个对象上触发某类事件，如果此对象绑定了事件，就会触发事件，如果没有，就会向这个对象的父级对象传播，最终父级对象触发了事件。

**事件捕获**本质上是利用了浏览器事件冒泡的机制。因为事件在冒泡过程中会上传到父节点，并且父节点可以通过事件对象获取到目标节点，因此可以把子节点的监听函数定义在父节点上，由父节点的监听函数统一处理多个子元素的事件，这种方式称为**事件代理**。

**事件代理**addEventListener(event, function, useCapture) 绑定一个事件处理函数？

**阻止事件冒泡**：

- 给子级加`event.stopPropagation()`：仅阻止冒泡
- 在事件处理函数中return false：不仅阻止了冒泡，同时阻止了事件本身
- 阻止默认事件：event.preventDefault( )

冒泡事件举例：

| touchstart         | 手指触摸动作开始                                             |                                                              |
| ------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| touchmove          | 手指触摸后移动                                               |                                                              |
| touchcancel        | 手指触摸动作被打断，如来电提醒，弹窗                         |                                                              |
| touchend           | 手指触摸动作结束                                             |                                                              |
| tap                | 手指触摸后马上离开                                           |                                                              |
| longpress          | 手指触摸后，超过350ms再离开，如果指定了事件回调函数并触发了这个事件，tap事件将不被触发 | [1.5.0](https://developers.weixin.qq.com/miniprogram/dev/framework/compatibility.html) |
| longtap            | 手指触摸后，超过350ms再离开（推荐使用longpress事件代替）     |                                                              |
| transitionend      | 会在 WXSS transition 或 wx.createAnimation 动画结束后触发    |                                                              |
| animationstart     | 会在一个 WXSS animation 动画开始时触发                       |                                                              |
| animationiteration | 会在一个 WXSS animation 一次迭代结束时触发                   |                                                              |
| animationend       | 会在一个 WXSS animation 动画完成时触发                       |                                                              |
| touchforcechange   | 在支持 3D Touch 的 iPhone 设备，重按时会触发                 |                                                              |

非冒泡事件：

除上述冒泡事件之外，如表单的submit，input中的input事件，scroll等都是非冒泡事件



### 普通函数和箭头函数的区别

1. 箭头函数是匿名函数，不能作为构造函数，不能使用new，没有super
2. 箭头函数不绑定`arguments`，取而代之用`rest`参数...解决
3. 箭头函数不绑定`this`，会捕获其所在的上下文的this值，作为自己的this值
4. 箭头函数通过 `call()或 apply()` 方法调用一个函数时，只传入了一个参数，对 this 并没有影响。
5. 箭头函数没有原型属性
6. 箭头函数不能当做`Generator`函数,不能使用`yield`关键字



### 类数组对象与arguments

**类数组对象**：拥有一个 length 属性和若干索引属性的对象，不能直接使用数组的方法，可用Function.call间接调用，比如：

```
var arrayLike = {0: 'name', 1: 'age', 2: 'sex', length: 3 }
Array.prototype.join.call(arrayLike, '&'); // name&age&sex
```

常见的类数组：

1. 用getElementsByTagName/ClassName()获得的HTMLCollection
2. 用querySelector获得的nodeList

将类数组转换成数组的方式：

- Array.prototype.slice.call()
- Array.from()
- ES6展开运算符...
- 利用concat+apply(将参数展开)

**Arguments对象**：函数的参数，length属性，callee属性(通过它调用函数自身)

ps：传入的参数，实参和 arguments 的值会共享，当没有传入时，实参与 arguments 值不会共享。除此之外，以上是在非严格模式下，如果是在严格模式下，实参和 arguments 是不会共享的。

闭包经典题：

```
var data = [];

for (var i = 0; i < 3; i++) {
    (data[i] = function () {
       console.log(arguments.callee.i) 
    }).i = i;
}
data[0]();
data[1]();
data[2]();
```

使用...符号将arguments转换为数组



### 数组方法

- 判断是否是数组的方法：
  1. Array.isArray() 
  2. instanceof
  3. constructor
  4. Object.prototype.toString.call()
- join：数组内值的拼接；concat：连接数组，浅拷贝，不影响原数组？
- forEach：


​	特点：return无效，会改变原数组。

​	中断该循环的方法：

1. 使用try监视代码块，在需要中断的地方抛出异常
2. (推荐)：用every和some替代

- foreach和map的区别：前者不会返回值，后者会返回新的数组。

判断数组中是否包含某个值：

1. array.indexOf()/lastIndexOf()
2. array.includes(searcElement[,fromIndex])
3. array.find(callback)
4. array.findIndex(callback)

数组的增删改：

1. push/pop
2. shift/unshift
3. slice(start, end) 浅拷贝，不会改变原数组
4. splice(start,deleteCount,item1,item2) 会改变原数组

数组排序：

1. sort(compare)：注意比较函数的书写

数组之函数式编程的方法：

1. map(fn(cur, index, array, thisArgs)) 返回新数组
2. filter(fn(element, index, array, thisArgs)) 返回新数组
3. reduce(reducer(acc, cur, idx, array)) 返回结果值

数组扁平化的方法：

1. 普通递归
2. ES6中的flat()方法
3. 利用reduce函数进行递归
4. 扩展运算符

数组之原型链方法：

1. toString
2. valueOf

### valueof & tostring

`valueOf` 和 `toString` 几乎都是在出现操作符`(+-*/==><)`时被调用(隐式转换)，具有自动调用和重写的性质。如果其中一边为对象，则会先调用`toSting`方法

- tostring：返回一个表示该对象的字符串，特殊：表示对象的时候，变成`[object Object]`，表示数组的时候，就变成数组内容以逗号连接的字符串。**字符串**运算中，优先调用了`toString`
- valueof：在**数值**运算中，优先调用了`valueOf`

注：*严格等于不会触发隐式转换

面试题：

1. 实现 a==1 && a==2 && a==3: 重写valueof或者tostring
2. 实现 a===1 && a===2 && a===3: 利用Object.defineProperty()进行数据劫持
3. 函数柯里化实现多参累加



### JS之高阶函数

基本概念：`一个函数`就可以接收另一个函数作为参数或者返回值为一个函数，`这种函数`就称之为高阶函数。

#### 数组中的高阶函数

1. map(fn[,this]) // args: item, index, array 小练习：实现map
2. reduce(fn, 初始值) // args: preSum, curVal, curIndex, array
3. filter(fn)
4. sort(compare()) //若不传比较函数，则按字符串大小排序



## 创建对象的多种方式

1. 工厂模式

   ```
   function createPerson(name) {
       var o = new Object();
       o.name = name;
       o.getName = function () {
           console.log(this.name);
       };
   
       return o;
   }
   
   var person1 = createPerson('kevin');
   ```

   缺点：对象无法识别，因为所有的实例都指向一个原型

2. 构造函数模式

   ```
   function Person(name) {
       this.name = name;
       this.getName = function () {
           console.log(this.name);
       };
   }
   
   var person1 = new Person('kevin');
   ```

   优点：实例可以识别为一个特定的类型

   缺点：每次创建实例时，每个方法都要被创建一次

3. 原型模式

   ```
   function Person(name) {
   
   }
   
   Person.prototype.name = 'keivn';
   Person.prototype.getName = function () {
       console.log(this.name);
   };
   
   var person1 = new Person();
   ```

   优点：方法不会重建

   缺点：所有的属性和方法都被共享，且不能初始化参数

   优化版1：

   ```
   function Person(name) {
   
   }
   
   Person.prototype = {
       name: 'kevin',
       getName: function () {
           console.log(this.name);
       }
   };
   
   var person1 = new Person();
   ```

   优点：封装性好了一点

   缺点：重写了原型，丢失了constructor属性

   

   优化版2：

   ```
   function Person(name) {
   
   }
   
   Person.prototype = {
       constructor: Person,
       name: 'kevin',
       getName: function () {
           console.log(this.name);
       }
   };
   
   var person1 = new Person();
   ```

   优点：实例可以通过constructor属性找到所属构造函数

   缺点：原型模式该有的缺点还是有

4. 组合模式

   ```
   function Person(name) {
       this.name = name;
   }
   
   Person.prototype = {//对象字面量
       constructor: Person,
       getName: function () {
           console.log(this.name);
       }
   };
   
   var person1 = new Person();
   ```

   优点：该共享的共享，该私有的私有，使用最广泛的方式

   缺点：有的人就是希望全部都写在一起，即更好的封装性

   

   优化版：动态原型模式

   ```
   function Person(name) {
       this.name = name;
       if (typeof this.getName != "function") {
           Person.prototype.getName = function () {
               console.log(this.name);
           }
       }
   }
   
   var person1 = new Person();
   ```

   注：不能用对象字面量重写原型or 以下这种方式

   ```
   function Person(name) {
       this.name = name;
       if (typeof this.getName != "function") {
           Person.prototype = {
               constructor: Person,
               getName: function () {
                   console.log(this.name);
               }
           }
   
           return new Person(name);
       }
   }
   
   var person1 = new Person('kevin');
   var person2 = new Person('daisy');
   
   person1.getName(); // kevin
   person2.getName();  // daisy
   ```

5. 寄生构造函数

   ```
   function Person(name) {//寄生在构造函数的一种方法。
       var o = new Object();
       o.name = name;
       o.getName = function () {
           console.log(this.name);
       };
       return o;
   }
   
   var person1 = new Person('kevin');
   console.log(person1 instanceof Person) // false
   console.log(person1 instanceof Object)  // true
   ```



## 垃圾回收机制

V8 将内存分成 **新生代空间** 和 **老生代空间**。

![img](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/aa2d5ad1d89b4b7b919f20e4a5f8973a~tplv-k3u1fbpfcp-watermark.awebp)

- 标记清除

  优点：实现比较简单，打标记分打与不打，即用一位二进制位（0和1）就可以为其标记，非常简单

  缺点：

  - 隔一段时间就需要标记清除，浏览器资源被占用。

  - 清除之后，剩余的对象内存位置是不变的，也会导致空闲内存空间是不连续的，出现 `内存碎片`，并且由于剩余空闲内存不是一整块，它是由不同大小内存组成的内存列表，这就牵扯出了内存分配的问题。

    解决方案：分块策略：最好的 first-fit，找到适合的立即返回。更优的解法是，清除一遍移动占内存的对象，使剩余内存连续。

- 引用计数

  优点：可以立即回收

  缺点：计数器需要占用资源，且无法解决循环引用的问题



## 内存泄露

- 意外的**全局变量**: 无法被回收
- **定时器**: 未被正确关闭，导致所引用的外部变量无法被释放
- **事件监听**: 没有正确销毁 (低版本浏览器可能出现)
- **闭包**: 会导致父级中的变量无法被释放
- **dom 引用**: dom 元素被删除时，内存中的引用未被正确清空



## JS手撕题

### typeof

Object.prototype.toString.call(obj)  

### 继承和原型链

Q:ES6之前使用prototype实现继承？

A：Object.create()+constructor重新指向

Q：为什么寄生组合式继承上的引用类型不会共享？

1. 原型链

   注：方法不能用箭头函数，会报undefined，可能是箭头函数没有this的原因？

   **查找顺序**：实例的构造函数，构造函数的原型， 原型的构造函数，以此类推

   **判断原型和实例的继承关系：**

   - intanceof
   - isPrototypeOf：eg. Object.prototype.isPrototypeOf(instance) 只要原型上出现过		

   **缺点：**

   问题一: 当原型链中包含引用类型值的原型时,该引用类型值会被所有实例共享.

   问题二: 在创建子类型(如创建Son的实例)时,不能向超类型(例如Father)的构造函数中传递参数

2. 借用构造函数

   基本思想:即在子类型构造函数的内部调用超类型构造函数

   eg. function Son(){ Father.call(this) }

   **优点：**解决了原型链的缺点

   **缺点：**只能从父类继承，不能从原型上继承；无法实现复用。

3. **组合继承**

   基本思想：将原型链和借用构造函数结合的方法。原型上继承原型属性和方法，构造函数上写实例属性。优点：很好的实现了方法，**缺点：**每次都会调用两次构造函数

4. 原型式继承

   ```
   function createObj(o) {
       function F(){}
       F.prototype = o;
       return new F();
   }
   ```

   ES5的Object.create()的实现，将传入的对象作为创建的对象的原型。

   **Object.create(arg1，arg2)**：

   ​		arg1:一个用作新对象原型的对象

   ​		arg2：一个为新对象定义额外属性的对象

   缺点：包含引用类型的属性值始终都会共享相应的值，且无法传递参数

5. 寄生式继承

   基本思想：在原型式继承基础上，增强对象，返回构造函数，缺点：同原型式继承。

   ```
   function createObj (o) {
       var clone = Object.create(o);
       clone.sayName = function () {
           console.log('hi');
       }
       return clone;
   }
   ```

6. **寄生式组合继承（最优）**

   基本思路是: 不必为了指定子类型的原型而调用父类的构造函数

   原始：

   ```
   function inheritPrototype(subClass,superClass){ 
   	var prototype = object(superClass.prototype);//创建对象 
   	prototype.constructor = subClass;//增强对象 
   	subClass.prototype = prototype;//指定对象 
   }
   // 父类初始化实例属性和原型属性
   function SuperType(name){
     this.name = name;
     this.colors = ["red", "blue", "green"];
   }
   SuperType.prototype.sayName = function(){
     alert(this.name);
   };
   
   // 借用构造函数传递增强子类实例属性（支持传参和避免篡改）
   function SubType(name, age){
     SuperType.call(this, name);
     this.age = age;
   }
   
   // 将父类原型指向子类
   inheritPrototype(SubType, SuperType);
   
   // 新增子类原型属性
   SubType.prototype.sayAge = function(){
     alert(this.age);
   }
   
   var instance1 = new SubType("xyc", 23);
   var instance2 = new SubType("lxy", 23);
   
   instance1.colors.push("2"); // ["red", "blue", "green", "2"]
   instance1.colors.push("3"); // ["red", "blue", "green", "3"]
   
   ```

7. 混入方式继承多个对象

   	function MyClass() {     
   		SuperClass.call(this);     
   		OtherSuperClass.call(this); 
   	} // 继承一个类 
   	MyClass.prototype = Object.create(SuperClass.prototype); // 混合其它 Object.assign(MyClass.prototype, OtherSuperClass.prototype); // 重新指定constructor MyClass.prototype.constructor = MyClass; 
   	MyClass.prototype.myMethod = function() {     // do something };
   
8. class实现继承 ES6

   extends，super，constructor，方法

注：

- 函数声明和类声明的区别：函数声明会提升，类声明不会。首先需要声明你的类，然后访问它，否则像下面的代码会抛出一个ReferenceError。
- 继承：ES5继承实质上是先创建子类的实例对象，再将父类方法添加到this上，再在子类中call(this)。ES6的继承有所不同，实质上是先创建父类的实例对象this，然后再用子类的构造函数修改this。因为子类没有自己的this对象，所以必须先调用父类的super()方法，否则新建实例报错。

### call & apply & bind

ps:

1. apply妙用：改变函数传入参数的形式，eg：Math.min.apply(null,array)
2. 绑定多个call，会选取第一个

代码流程：

- 将函数设为对象的属性
- 执行&删除这个函数
- 指定`this`到函数并传入给定参数执行函数
- 如果不传入参数，默认指向为 window

call的实现：

```
Function.prototype.call2 = function (context) {
    var context = context || window;//空参时，this指向window
    context.fn = this;//将函数变成对象属性，即改变this指向
	
	//可以优化成 ...args
    var args = [];//解决参数不定长-优化：扩展运算符
    for(var i = 1, len = arguments.length; i < len; i++) {
        args.push('arguments[' + i + ']');
    }

    var result = eval('context.fn(' + args +')');//eval拼成一个函数，执行

    delete context.fn //删除该函数
    return result;//返回函数的结果
}

//方法二
// call
Function.prototype.call = function (context, ...args) {
  context = context || window;
  
  const fnSymbol = Symbol("fn");
  context[fnSymbol] = this;
  
  context[fnSymbol](...args);
  delete context[fnSymbol];
}

```

apply的实现（和call原理相似）：

```
Function.prototype.apply = function (context, arr) {//参数不同
    var context = Object(context) || window;
    context.fn = this;

    var result;
    if (!arr) {
        result = context.fn();
    }
    else {
        var args = [];
        for (var i = 0, len = arr.length; i < len; i++) {
            args.push('arr[' + i + ']');
        }
        result = eval('context.fn(' + args + ')')
    }

    delete context.fn
    return result;
}

//方法二
// apply
Function.prototype.apply = function (context, argsArr) {
  context = context || window;
  
  const fnSymbol = Symbol("fn");
  context[fnSymbol] = this;
  
  context[fnSymbol](...argsArr);
  delete context[fnSymbol];
}

```

bind实现：

返回函数/传参/

```
Function.prototype.bind2 = function (context) {
	//调用bind的不是函数会出错
    if (typeof this !== "function") {
      throw new Error("Function.prototype.bind - what is trying to be bound is not callable");
    }
    
    var self = this;//改变this的指向
    //获取函数指定区域的参数[1:]
    var args = Array.prototype.slice.call(arguments, 1);
	
	//构造函数实现，因为bind返回的新函数可以使用new创建对象
    var fNOP = function () {};

    var fBound = function () {
    	//返回函数的参数
        var bindArgs = Array.prototype.slice.call(arguments);
         // 当作为构造函数时，this 指向实例，此时结果为 true，将绑定函数的 				this 指向该实例，可以让实例获得来自绑定函数的值
         // 当作为普通函数时，this 指向 window，此时结果为 false，将绑定函数的 			   this 指向 context
        return self.apply(this instanceof fNOP ? this : context, 						args.concat(bindArgs));
    }
	
    fNOP.prototype = this.prototype;
    // 修改返回函数的 prototype 为绑定函数的 prototype，实例就可以继承绑定函数		的原型中的值
    fBound.prototype = new fNOP();//用一个空函数作为中转
    return fBound;
}

//方案二
// apply

Function.prototype.apply = function (context, argsArr) {
  context = context || window;
  
  const fnSymbol = Symbol("fn");
  context[fnSymbol] = this;
  
  context[fnSymbol](...argsArr);
  delete context[fnSymbol];
}

```

### this

this是一个指针，指向调用函数的对象。指向调用它的地方， 严格模式和非严格模式不同。

`this`对象是是执行上下文中的一个属性，它指向最后一次调用这个方法的对象，在全局函数中，`this`等于`window`，而当函数被作为某个对象调用时，this等于那个对象。 在实际开发中，`this `的指向可以通过四种调用模式来判断。

1. 函数调用，当一个函数不是一个对象的属性时，直接作为函数来调用时，`this`指向全局对象。
2. 方法调用，如果一个函数作为一个对象的方法来调用时，`this`指向这个对象。(隐式绑定)，指向绑定的最后一层。
3. 构造函数调用，`this`指向这个用`new`新创建的对象。
4. DOM事件绑定：onclick和addEventListner中的this默认指向绑定事件中的元素
5. 第四种是 `apply 、 call 和 bind `调用模式，这三个方法都可以显示的指定调用函数的 this 指向。`apply`接收参数的是数组，`call`接受参数列表，`` bind`方法通过传入一个对象，返回一个` this `绑定了传入对象的新函数。这个函数的 `this`指向除了使用`new `时会被改变，其他情况下都不会改变。

注：若绑定null或者undefined，则忽略，应用默认绑定规则；settimeout(person.fn,)这时函数变成了变量，指向则找不到了；函数内的硬绑定；

**new绑定>(显示)硬绑定call,apply,bind关键字>隐式绑定XX.fn()>默认绑定**



### New操作到底做了什么？

1. var obj  = {}; 我们创建了一个空对象obj;

2. obj.__proto__ = F.prototype; 我们将这个空对象的__proto__成员指向了F函数对象prototype成员对象;

3. F.call(obj);我们将F函数对象的this指针替换成obj，然后再调用F函数.

   代码实现：

   ```
   function objectFactory() {
   	//对应步骤一
       var obj = new Object()//更好的方式：var obj = Object.create(null)
   	//取出第一个参数
       Constructor = [].shift.call(arguments);
   	//将obj的原型指向构造函数，来访问构造函数中的属性
       obj.__proto__ = Constructor.prototype;
   	//将构造函数绑定对象和参数
       var ret = Constructor.apply(obj, arguments);
   	//构造函数返回对象或者基本类型
       return typeof ret === 'object' ? ret : obj;
   
   };
   ```

### 数组去重

1. ES5做法：利用 filter(回调函数),indexOf()
2. ES6做法：利用Set的属性

### 数组扁平化

1. ES5：Array.isArray() + concat 
2. ES6: Array.some() **?没理解**



### 赋值和深浅拷贝（针对引用类型）

- 赋值：当我们把一个对象赋值给一个新的变量时，**赋的其实是该对象的在栈中的地址，而不是堆中的数据**。也就是两个对象指向的是同一个存储空间，无论哪个对象发生改变，其实都是改变的存储空间的内容，因此，两个对象是联动的。

- 浅拷贝：浅拷贝是创建一个新对象，这个对象有着原始对象属性值的一份精确拷贝。如果属性是基本类型，拷贝前后基本类型互不影响，如果属性是引用类型，拷贝的就是内存地址 ，所以如果其中一个对象改变了这个地址，就会影响到另一个对象。

  实现方式：

  1. 代码：typeof + {} + for in + hasOwnProperty
  2. object.assign(target, source,...)：
     - 只会拷贝源对象自身的并且可枚举的属性到目标对象。
     - source可以为undefined or null，但target不能是这两种。
     - 同名属性替换
     - 继承属性无法拷贝
  3. 展开运算符...
  4. Array.proyotype.concat() => 浅拷贝数组
  5. Array.proyotype.slice() => 浅拷贝数组

- 深拷贝：深拷贝是将一个对象从内存中完整的拷贝一份出来,从堆内存中开辟一个新的区域存放新对象,且修改新对象不会影响原对象。对对象中的子对象进行递归拷贝,拷贝前后的两个对象互不影响。

  实现方式：

  1. JSON.parse(JSON.stringfy()) ，但是

     - 不能解决循环引用(创建一个map/weakMap记录已经拷贝过的对象)；

     - 不能处理特殊的对象：RegExp, Date, Set, Map(分类型去处理);

     - 不能拷贝函数(普通函数和箭头函数的区分：原型，箭头函数没有原型)；
  2. 手写递归
     - 用什么保存拷贝的对象
     - 解决循环引用：weakmap
     - 特殊类型的处理：Array/Date/RegExp/Function

### 发布订阅模式

### 解析URL参数为对象

### 字符串模板

1. 给定一个正则表达式
2. reg.test() 查看给定的模板是否存在此reg，若没有，则直接返回。
3. 从模板中分离要代替的字符：reg.exec()
4. 代替字符，replace
5. 递归代替



### 懒加载和预加载

基本思想：懒加载也叫延迟加载，是指在长网页中延迟加载图像，是一种优化网页性能的方式。

**实现原理：**首先将页面上的图片的 src 属性设为空字符串，而图片的真实路径则设置在data-original属性中， 当页面滚动的时候需要去监听scroll事件，在scroll事件的回调中，判断我们的懒加载的图片是否进入可视区域(高度差),如果图片在可视区内将图片的 src 属性设置为data-original 的值，这样就可以实现延迟加载。

代码思路：

1. 设置img属性 src/lazyload/data-original

2. 监听：document.addEventListener()

3. 懒加载函数：

   - 挑选元素：querySelectorAll()

   - 判断元素是否出现在可视区域：

     ​		viewHeight = document.documentElement.clientHeight

   - 获取元素相对于浏览器视窗的位置：

     ​		item.getBoundingClientRect()

4. 移除相关属性：removeAttribute()



### 函数防抖

概念：在事件被触发n秒后再执行回调，如果在这n秒内又被触发，则重新计时。

```
function debounce(fn, delay) {
    return function (args) {
        let that = this
        let _args = args
        clearTimeout(fn.time)//我的理解是清除之前的时间
        fn.time = setTimeout(function () {
            fun.call(that, _args)
        }, delay)
    }
}
ps：注意监听的事件以及它对应的输出
```

### 函数节流

概念：规定在一个单位时间内，只能触发一次函数。如果这个单位时间内触发多次函数，只有一次生效。

```
  function throttle(fun, delay) {
        let last, deferTimer
        return function (args) {
            let that = this
            let _args = arguments
            let now = +new Date()
            if (last && now < last + delay) {//这块的逻辑是，如果时间还没到，则settimeout
                clearTimeout(deferTimer)//清除上次的计时
                deferTimer = setTimeout(function () {
                    last = now
                    fun.apply(that, _args)
                }, delay)
            }else {//否则，立即执行函数
                last = now
                fun.apply(that,_args)
            }
        }
    }
```

防抖应用：

- 登录、发短信等按钮避免用户点击太快，以致于发送了多次请求，需要防抖
- 调整浏览器窗口大小时，resize 次数过于频繁，造成计算过多，此时需要一次到位，就用到了防抖
- 文本编辑器实时保存，当无任何更改操作一秒后进行保存

节流应用：

- scroll 事件，每隔一秒计算一次位置信息等
- 浏览器播放事件，每隔一秒计算一次进度信息等
- input 框实时搜索并发送请求展示下拉列表，每隔一秒发送一次请求



### Promise

如何解决回调地狱：

- 回调函数延迟绑定
- 返回值穿透
- 错误冒泡

方法：

- new Promise(fn(resolve, reject))
- then
- catch：捕获第一个异常
- finally(一定会执行)
- all：并行执行
- race：并行执行，只保留第一个执行完成的结果。应用：超时处理
- any
- Promise.resolve()/.reject()

ps: promise可以捕获错误，但不会中断外部程序的允许，没有捕获就会因为错误中断程序

代码思路：

1. promise只执行一次，执行resolve,变fulfilled,执行reject,变rejected,throw == reject;executor + result + state
2. 实现then:then接受两个回调，一个成功回调，状态为fulfilled，一个失败回调，状态为rejected，如果resolve或reject在定时器里，则定时器结束再执行then，then支持链式调用，下一次then受上次的then的返回值影响；function＋callback＋
3. 实现链式调用

Q：为什么promise要引入微任务？

A：使用异步回调，将回调函数放到`当前宏任务中`的最后面，解决了两大痛点：

- 采用**异步回调**替代同步回调解决了浪费 CPU 性能的问题。
- 放到**当前宏任务最后**执行，解决了回调执行的实时性问题。

### async 和 await

 async 是一个通过异步执行并隐式返回 Promise 作为结果的函数。

Q：forEach中用await会怎样？

A：循环里面执行的代码会乱序。解决方案：for-of(本质是迭代器，保证了执行的顺序)

**如果在async函数中抛出了错误，则终止错误结果，不会继续向下执行。**如果想要使得错误的地方不影响`async`函数后续的执行的话，可以使用`try catch`

### 

### 生成器

概念：一个像函数的对象， 有next() value & done，遇到 yeild，next()方法才暂停

原理：协程，线程的下一个量级。一个线程只能执行一个协程

thunk函数：定制化函数



### 堆和栈

**栈(stack)：**是栈内存的简称，栈是**自动分配**相对**固定大小**的内存空间，并由系**统自动释放，**栈**数据结构**遵循**FILO**（first in last out）**先进后出**的原则。栈的特点：开口向上、速度快,容量小。

**堆(heap)：**是堆内存的简称，堆是**动态分配**内存，**内存大小不固定**，也**不会自动释放，**堆**数据结构**是一种无序的树状结构，同时它还满足key-value键值对的存储方式；我们只用知道key名，就能通过key查找到对应的value。堆的特点：速度稍慢、容量比较大；



### ajax原理

Async Javascript and XML，`Ajax`的原理简单来说通过`XmlHttpRequest`对象来向服务器发异步请求，从服务器获得数据，然后用`JavaScript`来操作`DOM`而更新页面

传统的Web应用交互由用户触发一个HTTP请求到服务器(浪费带宽)，AJAX应用可以仅向服务器发送并取回必需的数据

优点：

- 无刷新更新数据
- 异步与服务器通信
- 前端和后端负载平衡
- 基于标准被广泛支持
- 界面与应用分离

缺点：

- AJAX干掉了Back和History功能，即对浏览器机制的破坏
- AJAX的安全问题
- 对搜索引擎支持较弱
- 破坏程序的异常处理机制
- 违背URL和资源定位的初衷



### Q：描述一下v8执行一段js代码的过程

解释器语言对源码做的分析：

- 通过词法分析和语法分析生成 AST(抽象语法树)：词法分析和语法分析
- 生成字节码(更加轻量，省去了生成二进制文件的操作，降低内存的压力)
- 解释器执行字节码



### Q:如何判断一个对象是否为空？

1. JSON.stringfy(data) === '{}')
2. for in 循环遍历key
3. Object.getOwnPropertyNames()  返回一个属性数组
4. Object.keys() — ES6方法 返回一个属性数组



### 其他

1. DMZ

2. 实现一个pipe函数，`pipe`是可以接收任意个数的函数，并且返回的是一个新的函数`res`。

3. 让<p>测试 空格</p>的空格间隙变大：

   - word-spacing/letter-spacing
   - 利用span包裹空格，然后再设置word-spacing/letter-spacing

4. 如何解决inline-block空白问题？

   - **删除html中的空白**：不要让元素之间换行

   - **margin-left**: -0.4em;

   - 父级：font-size 子级若有文字需单独设置字体




### 设计模式

- 工厂模式：解决多个类似对象声明的问题；
- 复杂的工厂模式：将成员对象的实例化推迟到子类中，重写父类接口。
- 单体模式：
  1. 可以用来划分命名空间，减少全局变量的数量
  2. 可以使代码组织的更为一致，使代码容易阅读和维护
  3. 可以被实例化，且只能实例化一次
- 模块模式
- 代理模式



Q:input事件和change事件的区别？

- Input: 输入字符时触发（不包含功能性按键， enter， control 等)
- Change: 失去焦点且当前的值跟上次触发的值不同 或者 enter键被触发且当前的值跟上次触发的值不同



## 代码复用

1. 函数封装
2. 原型继承
3. 复制所有属性进行继承(深浅拷贝)
4. mix in 混合好几个属性
5. 借用方法 call apply bind



## AST

抽象语法树

### Babel处理流程

![img](https://p1-jj.byteimg.com/tos-cn-i-t2oaga2asx/gold-user-assets/2019/10/2/16d8d0cd559c7e1e~tplv-t2oaga2asx-watermark.awebp)

### Babel架构

![img](https://p1-jj.byteimg.com/tos-cn-i-t2oaga2asx/gold-user-assets/2019/10/2/16d8d0cd5a3f3a0c~tplv-t2oaga2asx-watermark.awebp)

1. 内核的工作：
   - 加载和处理配置(config)
   - 加载插件
   - 调用 `Parser` 进行语法解析，生成 `AST`
   - 调用 `Traverser` 遍历AST，并使用`访问者模式`应用'插件'对 AST 进行转换
   - 生成代码，包括SourceMap转换和源代码生成
2. 核心周边支持
   - Parser：将源代码解析为AST
   - Traverser：实现了**访问者模式**
   - Generator： 将 AST 转换为源代码，支持 SourceMap
3. 插件/插件开发辅助/工具

### 访问者模式

概念：**所以转换器操作 AST 一般都是使用`访问器模式`，由这个`访问者(Visitor)`来 ① 进行统一的遍历操作，② 提供节点的操作方法，③ 响应式维护节点之间的关系；而插件(设计模式中称为‘具体访问者’)只需要定义自己感兴趣的节点类型，当访问者访问到对应节点时，就调用插件的访问(visit)方法**。

流程：

1. 节点的遍历
2. 节点的上下文
3. 副作用处理：新旧节点替换后的处理
4. 作用域的处理



### webpack

1. 作用

   - 模块打包：保证不同模块之间的正确引用
   - 编译兼容：Loader机制(进行文件的转换)
   - 能力扩展：Plugin机制(功能扩展)

2. 打包流程

   1. 读取`webpack`的配置参数；
   2. 启动`webpack`，创建`Compiler`对象并开始解析项目；
   3. 从入口文件（`entry`）开始解析，并且找到其导入的依赖模块，递归遍历分析，形成依赖关系树；
   4. 对不同文件类型的依赖模块文件使用对应的`Loader`进行编译，最终转为`Javascript`文件；
   5. 整个过程中`webpack`会通过发布订阅模式，向外抛出一些`hooks`，而`webpack`的插件即可通过监听这些关键的事件节点，执行插件任务进而达到干预输出结果的目的。

   在`webpack`源码中主要依赖于`compiler`和`compilation`两个核心对象实现。

   `compiler`对象是一个全局单例，负责把控整个`webpack`打包的构建流程。 `compilation`对象是每一次构建的上下文对象，它包含了当次构建所需要的所有信息，每次**热更新**和重新构建，`compiler`都会重新生成一个新的`compilation`对象，负责此次更新的构建过程。

3. sourceMap

   `sourceMap`是一项将编译、打包、压缩后的代码映射回源代码的技术，由于打包压缩后的代码并没有阅读性可言，一旦在开发中报错或者遇到问题，直接在混淆代码中`debug`问题会带来非常糟糕的体验，`sourceMap`可以帮助我们快速定位到源代码的位置，提高我们的开发效率。`sourceMap`其实并不是`Webpack`特有的功能，而是`Webpack`支持`sourceMap`，像`JQuery`也支持`souceMap`。

4. Loader

5. Plugin


























