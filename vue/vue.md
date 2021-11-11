https://juejin.cn/post/6961222829979697165

https://juejin.cn/post/6844903918753808398

- ### VUE

- 核心特性：数据驱动、组件化、指令系统

- 单页面应用：仅在 Web 页面初始化时加载相应的 HTML、JavaScript 和 CSS。一旦页面加载完成，SPA 不会因为用户的操作而进行页面的重新加载或跳转；取而代之的是利用路由机制实现 HTML 内容的变换，UI 与用户的交互，避免页面的重新加载。

- **MVC**

  Model-View-Controller，即依靠Controller传递数据

- **MVVM**

  概念：**MVVM**是`Model-View-ViewModel`缩写，也就是把`MVC`中的`Controller`演变成`ViewModel(一切操作通过它)。Model`层代表数据模型，`View`代表UI组件，`ViewModel`是`View`和`Model`层的桥梁，数据会绑定到`viewModel`层并自动将数据渲染到页面中，视图变化的时候会通知`viewModel`层更新数据。**数据驱动**

  ps：$refs 这一属性让model可以直接操作view (所谓的不完全MVVM)

- **为什么 data 是一个函数**

  组件中的 data 写成一个函数，数据以函数返回值形式定义(函数返回的对象内存地址并不相同)，这样每复用一次组件，就会返回一份新的 data，类似于给每个组件实例创建一个私有的数据空间，让各个组件实例维护各自的数据。而单纯的写成对象形式，就使得所有组件实例共用了一份 data，就会造成一个变了全都会变的结果

- **Vue组件通信的方式**
  1. props 和$emit 父组件向子组件传递数据是通过 prop 传递的，子组件传递数据给父组件是通过$emit 触发事件来做到的
  2. $parent,$children 获取当前组件的父组件和当前组件的子组件
  3. $attrs 和$listeners A->B->C(值传递)。Vue 2.4 开始提供$attrs 和$listeners 来解决这个问题
  4. 父组件中通过 provide 来提供变量，然后在子组件中通过 inject 来注入变量。
  5. $refs 获取组件实例
  6. envetBus 兄弟组件数据传递 这种情况下可以使用事件总线的方式
  7. vuex 状态管理

- **生命周期**

  1. create阶段：vue实例被创建；**beforecreated**：在实例初始化之后，数据观测(data observer) 和 event/watcher 事件配置之前被调用。此时data和method中的数据都还没初始化；**created**：实例创建完毕，data中已经有数据，但还未挂载
  2. mount阶段：vue实例被挂载到真实DOM节点；**beforemount**：相关render函数被首次调用，可以发起服务端请求，获取数据；**mounted**：此时可以操作DOM
  3. update阶段：当vue实例里面的data数据变化时，触发组件的重新渲染。**beforeupdate**：数据更新时调用，发生在虚拟 DOM 重新渲染和打补丁（patch）之前。可以在这个钩子中进一步地更改状态，这不会触发附加的重渲染过程；**updated**：发生在更新完成之后，当前阶段组件 Dom 已完成更新。要注意的是避免在此期间更改数据，因为这可能会导致无限循环的更新，该钩子在服务器端渲染期间不被调用。
  4. destroy阶段：vue实例被销毁；**beforedestroy**：实例被销毁前调用，我们可以在这时进行善后收尾工作，比如清除计时器；**destroyed**， 实例销毁后调用。Vue 实例指示的所有东西都会解绑定，所有的事件监听器会被移除，所有的子实例也会被销毁。 该钩子在服务器端渲染期间不被调用。

  可以在钩子函数 **created**、beforeMount、mounted 中进行异步请求，因为在这三个钩子函数中，data 已经创建，可以将服务端端返回的数据进行赋值。

  推荐使用created：减少页面loading时间，同时ssr中也不存在另外两个钩子函数

- **vue的父子组件生命周期钩子函数执行顺序**

  - 加载渲染过程：父 beforeCreate->父 created->父 beforeMount->子 beforeCreate->子 created->子 beforeMount->子 mounted->父 mounted
  - 子组件更新过程：父 beforeUpdate->子 beforeUpdate->子 updated->父 updated
  - 父组件更新过程：父 beforeUpdate->父 updated
  - 销毁过程：父 beforeDestroy->子 beforeDestroy->子 destroyed->父 destroyed

- **vue-router 路由模式有几种？**

  - hash:  使用 URL hash 值来作路由。支持所有浏览器，包括不支持 HTML5 History Api 的浏览器；

    实现原理：location.hash

  - history :  依赖 HTML5 History API 和服务器配置。具体可以查看 HTML5 History 模式；

    实现原理：history.pushState() 和 history.repalceState()

  - abstract :  支持所有 JavaScript 运行环境，如 Node.js 服务器端。如果发现没有浏览器的 API，路由会自动强制进入这个模式

- SSR优缺点

  - 优点：可以被爬虫读取数据
  - 缺点：支持的生命周期函数比较有限

- **v-if & v-show**

  v-if 在编译过程中会被转化成三元表达式,条件不满足时不渲染此节点。(动态添加)，事件销毁

  v-show 会被编译成指令，条件不满足时控制样式将对应节点隐藏 （display:none）

- **class和style如何动态绑定？**

  Class 可以通过对象语法和数组语法进行动态绑定

- **内置指令**

  - v-once：只渲染一次，可视为静态元素
  - v-cloak：保持在元素上直到关联实例结束编译，用于解决初始化慢导致页面闪动的问题
  - v-on：用于监听DOM事件，eg: v-on:click, v-on:keyup
  - v-if/v-else/v-else-if：配合template使用，或是在render函数里面的三元表达式
  - v-if/v-show：判断是否隐藏；
  - v-for：数据循环出来；优先级比v-if高，注意增加唯一key
  - v-bind:class：绑定一个属性；
  - v-model：实现双向绑定，value和input语法糖
  - v-html：赋值的变量就是innerHTML，注意防止xss攻击
  - v-text：更新元素的textContent
  - v-pre：跳过这个元素以及子元素的编译过程

- **v-for中key的作用**

  1. 更高效的对比虚拟DOM的节点是否是相同节点，diff
  2. 判断节点：元素和key，当key的值不确定时，则它的值为undefined，则会一直去更新它

- **vue中的单向数据流**

  数据总是从父组件传到子组件，子组件没有权利修改父组件传过来的数据，只能请求父组件对原始数据进行修改。这样会防止从子组件意外改变父级组件的状态，从而导致你的应用的数据流向难以理解。

- **computed** ＆**watch**

  computed：计算属性，依赖其他计算属性，当函数所依赖的属性无变化时，则结果从缓存中读取。可以设置getter和setter。

  watch：观察key绑定的属性，主要用于监听某些特定数据的变化，进而执行相关操作

  

- **双向绑定实现原理**

  使用**数据劫持和发布订阅**模式实现的：

  View 变化更新 Data ，可以通过事件监听的方式来实现。而Data 变化如何更新 View？

  - 实现一个监听器 Observer：对数据对象进行遍历，包括子属性对象的属性，利用 Object.defineProperty() 对属性都加上 setter 和 getter。这样的话，给这个对象的某个值赋值，就会触发 setter，那么就能监听到了数据变化。
  - 实现一个解析器 Compile：解析 Vue 模板指令，将模板中的变量都替换成数据，然后初始化渲染页面视图，并将每个指令对应的节点绑定更新函数，添加监听数据的订阅者，一旦数据有变动，收到通知，调用更新函数进行数据更新。
  - 实现一个订阅者 Watcher：Watcher 订阅者是 Observer 和 Compile 之间通信的桥梁 ，主要的任务是订阅 Observer 中的属性值变化的消息，当收到属性值变化的消息时，触发解析器 Compile 中对应的更新函数。
  - 实现一个订阅器 Dep：订阅器采用 发布-订阅 设计模式，用来收集订阅者 Watcher，对监听器 Observer 和 订阅者 Watcher 进行统一管理。
  - ![1.png](https://p1-jj.byteimg.com/tos-cn-i-t2oaga2asx/gold-user-assets/2019/8/19/16ca75871f729d89~tplv-t2oaga2asx-watermark.awebp)

  

- **v-model的实现以及它的实现原理**

  通过event.target.value

  1. vue中双向绑定是一个指令`v-model`，可以绑定一个动态值到视图，同时视图中变化能改变该值。`v-model`是语法糖，默认情况下相于:`value和@input`。
  2. `v-model`可以减少大量繁琐的事件处理代码，提高开发效率，代码可读性也更好
  3. 通常在表单项上使用`v-model`
  4. 原生的表单项可以直接使用`v-model`，自定义组件上如果要使用它需要在组件内绑定value并处理输入事件
  5. 我做过测试，输出包含`v-model`模板的组件渲染函数，发现它会被转换为value属性的绑定以及一个事件监听，事件回调函数中会做相应变量更新操作，这说明神奇魔法实际上是vue的编译器完成的。

  

- **Vue中如何检测数组变化**

  Q:直接给一个数组项赋值，vue能检测到变化吗？不能

  对 7 种数组（push,shift,pop,splice,unshift,sort,reverse）方法进行重写(AOP 切片思想)

- **Vue中的diff算法**

  基本思想：虚拟DOM，对应的新旧Vnode，**diff**的过程就是调用`patch`函数比较新旧节点待补充

- **Vue性能优化**

  1. 尽量减少data中的数据
  2. key唯一
  3. 防抖，节流SS
  4. 第三方模块按需导入
  5. 图片懒加载
  6. 服务端渲染

- **实现双向绑定Proxy和Object.defineProperty的区别**

  1. **Object.definedProperty**的作用是劫持一个对象的属性，劫持属性的getter和setter方法，在对象的属性发生变化时进行特定的操作。而 Proxy劫持的是整个对象。
  2. **Proxy**会返回一个代理对象，我们只需要操作新对象即可，而Object.defineProperty只能遍历对象属性直接修改。
  3. **Object.definedProperty**不支持数组的各种API，而Proxy可以支持数组的各种API。
  4. 尽管Object.defineProperty有诸多缺陷，但是其兼容性要好于Proxy。
  
- **vue3.0特性**

  1. 响应式原理的改变 Vue3.x 使用 Proxy 取代 Vue2.x 版本的 Object.defineProperty
  2. 组件选项声明方式 Vue3.x 使用 Composition API setup 是 Vue3.x 新增的一个选项， 他是组件内使用 Composition API 的入口。
  3. 模板语法变化 slot 具名插槽语法 自定义指令 v-model 升级
  4. 其它方面的更改 Suspense 支持 Fragment（多个根节点）和 Protal（在 dom 其他部分渲染组建内容）组件，针对一些特殊的场景做了处理。 基于 treeshaking 优化，提供了更多的内置功能。

  

- **虚拟DOM**

  优点：

  1. 保证性能下限
  2. 无需手动操纵DOM
  3. 跨平台

  缺点：

  1. 无法机智优化
  2. 相对innerHTML来说会慢一点

- 虚拟DOM实现原理

  - 用 JavaScript 对象模拟真实 DOM 树，对真实 DOM 进行抽象；
  - diff 算法 — 比较两棵虚拟 DOM 树的差异；
  - patch 算法 — 将两个虚拟 DOM 对象的差异应用到真正的 DOM 树。

- **vue事件绑定原理**

  原生事件绑定是通过 addEventListener 绑定给真实元素的，组件事件绑定是通过 Vue 自定义的$on 实现的。如果要在组件上使用原生事件，需要加.native 修饰符，这样就相当于在父组件中把子组件当做普通 html 标签，然后加上原生事件。

  $on、$emit 是基于发布订阅模式的，维护一个事件中心，on 的时候将事件按名称存在事件中心里，称之为订阅者，然后 emit 将对应的事件进行发布，去执行事件中心里的对应的监听器

- **SPA**

  SPA（ single-page application ）仅在 Web 页面初始化时加载相应的 HTML、JavaScript 和 CSS。一旦页面加载完成，SPA 不会因为用户的操作而进行页面的重新加载或跳转；取而代之的是利用路由机制实现 HTML 内容的变换，UI 与用户的交互，避免页面的重新加载。

  

- **vue-router路由钩子函数的执行顺序**

- vue中的key有什么作用

  





















