https://juejin.cn/post/6844903988073070606#heading-22



### 声明式编程 & 命令式编程

前者关注做什么如html/SQL，后者关注怎么做。

### 函数式编程

属于声明式编程的一部分

- 不可变性：不能更改源数据，只能复制之后再进行更改。
- 纯函数：始终接受一个或多个参数并计算参数并返回数据或函数的函数。 它没有副作用，例如设置全局状态，更改应用程序状态，它总是将参数视为不可变数据。
- 数据转换：有副本
- 高阶函数：将函数作为参数的函数

### 框架的好处

- 组件化
- 开发效率

### 虚拟DOM

虚拟 DOM (VDOM)是真实 DOM 对应的JavaScript对象。对VDOM进行比较，若更新，则更新真实DOM。

优点：

- 保证性能下限
- 无需手动操作DOM
- 跨平台

缺点：无法极致优化



### 虚拟DOM和真实DOM

diff算法



### 生命周期

![img](https://p1-jj.byteimg.com/tos-cn-i-t2oaga2asx/gold-user-assets/2019/12/15/16f0a0b3e20fa9aa~tplv-t2oaga2asx-watermark.awebp)

广义划分：挂载阶段Mounting，更新阶段Updating，卸载阶段Unmounting

1. static **getDerivedStateFromProps**

   - **该生命周期钩子的作用：** 将父组件传递过来的 `props` **映射** 到子组件的 `state` 上面，这样组件内部就不用再通过 `this.props.xxx` 获取属性值了，统一通过 `this.state.xxx` 获取。映射就相当于拷贝了一份父组件传过来的 `props` ，作为子组件自己的状态。注意：子组件通过 `setState` 更新自身状态时，不会改变父组件的 `props`

   - 配合 `componentDidUpdate`，可以覆盖 `componentWillReceiveProps` 的所有用法

   - **该生命周期钩子触发的时机：**

     在 React 16.3.0 版本中：在组件实例化、接收到新的 `props` 时会被调用

     在 React 16.4.0 版本中：在组件实例化、接收到新的 `props` 、组件状态更新时会被调用

2. **componentDidMount**

   在第一次渲染之后执行，可以在这里做AJAX请求，DOM 的操作或状态更新以及设置事件监听器

3. **componentDidUpdate**

   `componentDidUpdate`(更新DOM)生命周期方法

4. **componentWillUnmount**

   componentWillUnmount(用于取消任何的网络请求，或删除与组件关联的所有事件监听器)

   

### setState是同步还是异步的

1. setState只在合成事件和钩子函数中是“异步”的，在原生事件和 setTimeout 中都是同步的。
2. setState的“异步”并不是说内部由异步代码实现，其实本身执行的过程和代码都是同步的，只是合成事件和钩子函数的调用顺序在更新之前，导致在合成事件和钩子函数中没法立马拿到更新后的值，形式了所谓的“异步”，当然可以通过第二个参数 setState(partialState, callback) 中的callback拿到更新后的结果。
3. setState的批量更新优化也是建立在“异步”（合成事件、钩子函数）之上的，在原生事件和setTimeout 中不会批量更新，在“异步”中如果对同一个值进行多次 setState ， setState 的批量更新策略会对其进行覆盖，取最后一次的执行，如果是同时 setState 多个不同的值，在更新时会对其进行合并批量更新。



### React组件之间通信方式

1. 父子组件,父->子直接用`Props`,子->父用`callback`回调
2. 跨层级通信：Context
3. 非父子组件,用发布订阅模式的`Event`模块
4. 项目复杂的话用`Redux、Mobx`等全局状态管理管库



## hooks

hooks只能在react函数最外层中调用：因为hook是依赖其**调用顺序**来对应每个state的；只能在函数组件中使用。

 useState(): 代替类组件中的state。返回一个元组

useContext()：解决prop drilling

useEffect()：数据获取，设置订阅，手动更改React组件中的DOM都属于副作用。和class组件中的生命周期函数componentDidMount-componentDidUpdate-componentWillUnmount的作用一样，但effect将这三个生命周期函数融合到一个API中。分为无需清除的effect和需要清除的effect。在effect中返回一个函数，则代表清除这个effect(可选项)。

useHistory ()

useRequest()

useCallback(fn, deps):  fn是一个函数，实现你需要做的事情， deps是一个fn中依赖的参数



### React中的组件

- 类组件/有状态组件

  概念：具有状态和生命周期方可能通过`setState()`方法更改组件的状态。

- 函数组件/无状态组件/展示组件

  函数或无状态组件是一个纯函数，它可接受接受参数，并返回react元素。

  函数组件和类组件的区别：

  1. 生命周期：函数组件不存在生命周期；类组件的生命周期钩子函数继承自React.Component;
  2. 状态管理：当组件只是接收 `props` 渲染到页面时，就是无状态组件；在React Hook出现之前，函数组件无状态(state)；类组件有状态state；
  3. React调用方式：函数组件直接调用； 类组件需要实例化，调用实例的render()方法；
  4. 获取渲染的数据：类组件的this指向会变化；函数组件没有this；

- 受控组件

  概念：自己维护 state，并根据用户输入进行更新。一般来说，表单元素<input><textarea>和<select>通常自己维护自己的状态，并根据用户输入进行更新。而在React中，包含表单的组件将跟踪其状态中的输入值，并在每次回调函数(例如`onChange`)触发时重新渲染组件，因为状态被更新。这种由 React 控制其值的输入表单元素称为**受控组件**。

- 高阶组件

  高阶组件(HOC)是接受一个组件并返回一个新组件的函数

  用处：

  1. 修改props
  2. 与其他组件一起封装，实现常用组件的复用
  3. 抽离state
  4. 反向继承
  5. 劫持渲染
  6. 多个参数

- 非受控组件

  概念：非受控组件是由 DOM 处理表单数据的地方，而不是在 React 组件中。通过ref

### React中的refs

应用：除props之外，在典型数据流之外，强制修改子代数据

`Refs` 提供了一种访问在`render`方法中创建的 DOM 节点或者 React 元素的方法。可用于类组件和函数组件

组件中添加ref属性，该属性的值为一个回调函数(类)

创建refs：React.createRef()



### React 中如何处理事件

`SyntheticEvent`是 React 跨浏览器的浏览器原生事件包装器，它还拥有和浏览器原生事件相同的接口，包括 `stopPropagation()` 和 `preventDefault()`



### props和state的区别

`props`和`state`是普通的 JS 对象。有state的叫做有状态组件，否则叫无状态组件

区别：

- 外部传入数据参数，不可变/数据管理：自己管理数据，控制状态，可变

补充：

为何不直接更新state(如 this.state.message = 'hello ')而是要利用setState()方法来做呢？

前者组件不会重新渲染



### super()

在调用`super()`方法之前，子类构造函数无法使用this引用，将 `props` 参数传递给 `super()` 调用的主要原因是在子构造函数中能够通过`this.props`来获取传入的 `props`。

注意：`props` 的行为只有在构造函数中是不同的，在构造函数之外访问是一样的



### JSX

将原始 HTML 模板嵌入到 JS 代码中。JSX 代码本身不能被浏览器读取，必须使用`Babel`和`webpack`等工具将其转换为传统的JS。是一个语法糖。使用的是React.createElement和document.createElement()

```
React.createElement(
  type, //标签类型/组件名
  [props],
  [...children]
)
```



### 如何避免组件的重新渲染？

- `React.memo()`:这可以防止不必要地重新渲染函数组件
- `PureComponent`:这可以防止不必要地重新渲染类组件



### React中的StrictMode

React 的`StrictMode`是一种辅助组件，可以帮助咱们编写更好的 react 组件，可以使用`<StrictMode />`包装一组组件，主要用于检查



### 路由模式

- 哈希路由HashRouter：利用hash实现路由跳转

- 浏览器路由BrowserRouter：利用h5 Api实现路由切换，借助history

  

### React fiber

React Fiber 是一种基于浏览器的单线程调度算法，协调引擎或重新实现核心算法。主要是**任务分割**

### 额外补充

ES6不提供自动绑定



待补充（redux）

### React

- **react中key的作用**

  基本思想：Keys是React用于追踪哪些列表中元素被修改、被添加或者被移除的辅助标识。

- 如何解析jsx

  调用React.createElement函数创建对象

- **关于react的优化方法**

  - 代码层面

    使用return null而不是CSS的display:none来控制节点的显示隐藏。保证同一时间页面的DOM节点尽可能的少。

  - props和state的数据尽可能简单明了，扁平化。

  - 代码体积

- redux



class一般结构

constructor

handleToggleClick

render()

ReactDOM.render()



## React.Component子类 React.FC函数式组件

每个组件通过render()方法返回需展示在页面上的层次结构



## state

构造函数是唯一可以给this.state赋值的地方

this.state({comment:"hello"})

state更新可能是异步的，让setState()接受一个函数（箭头或普通）而不是一个对象



## 事件处理

- React 事件的命名采用小驼峰式（camelCase），而不是纯小写。
- 使用 JSX 语法时你需要传入一个函数作为事件处理函数，而不是一个字符串。
- 在 React 中另一个不同点是你不能通过返回 `false` 的方式阻止默认行为。需使用preventDefault



## 条件渲染

&& ,三目运算符



## 列表 & key

key如何帮助识别哪些元素改变？一个列表有key一个没有，他们执行上会有什么区别呢？

多次渲染

key帮助识别哪些元素变了，就近定义

经验法则：在map方法中的元素需要设置key属性

key会传递信息给React但不会传递给你的组件

key在兄弟结点中必须唯一



## Dialog用法

Dialog.Base<>  基本框架

Dialog.Title 标题

<Dialog.Content> 内容：输入框 标签等无响应动作

Dialog.Actions 相应动作



## button 

type plain round circle 按钮的样式



## React.createRef()

Refs引用提供一个获得DOM节点或者创建在render方法中的React元素的方法

创建ref： ref = React.createRef()

  ref的值根据节点类型的不同而不同：

-   当ref属性用于HTML元素，在构造器中通过React.createRef()函数创建的ref接收底层DOM元素作为它的current属性；
-   当ref属性用于传统的类组件，ref对象接收挂载好的组件实例作为它的current；
-   你不能将ref属性用于函数式组件上，因为他们并没有实例（instance）！



Q:直接给初始数据和发出请求获取数据，渲染的时候有什么不同吗？





## File API

## 状态提升

## SPA



