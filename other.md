## js基础非常重要+热情+成果

## 看什么书？

## 工作之余会干什么？

## 你写的blog，通俗易懂吗？





### react 和 vue 的对比？

- 背景:以动态创建和交互式 UI 的能力而闻名/Vue 被设计为可以自底向上逐层应用，增量开发的设计。Vue 的核心库只关注视图层.
- 核心思想(组件化)：props变化时，父子组件都会重新渲染，也可以设置shouldComponentUpdate不渲染(没有vue性能好)/经典的html(结构)+css(表现)+js(行为)的形式/函数式的思想，组件使用jsx语法，即所有都融入js中。当state
- 数据绑定：react是单向数据流，react中属性是不允许更改的，状态是允许更改的/vue是实现了双向数据绑定的mvvm框架。
- diff算法的差异：
  1. react中diff算法实现流程
     - DOM结构发生改变-----直接卸载并重新create
     - DOM结构一样-----不会卸载,但是会update变化的内容
     - 所有同一层级的子节点.他们都可以通过key来区分-----同时遵循1.2两点
        （其实这个key的存在与否只会影响diff算法的复杂度,换言之,你不加key的情况下,diff算法就会以暴力的方式去根据一二的策略更新,但是你加了key,diff算法会引入一些另外的操作）
  2. vue中地方算法实现流程
     - 在内存中构建虚拟dom树
     - 将内存中虚拟dom树渲染成真实dom结构
     - 数据改变的时候，将之前的虚拟dom树结合新的数据生成新的虚拟dom树
     - 将此次生成好的虚拟dom树和上一次的虚拟dom树进行一次比对（diff算法进行比对），来更新只需要被替换的DOM，而不是全部重绘。在Diff算法中，只平层的比较前后两棵DOM树的节点，没有进行深度的遍历。
     - 将对比出来的差异进行重新渲染
- 数据管理：props支持传递静态或动态props，使用state来管理组件内的数据/props支持传递静态或动态props，使用data来管理组件的数据
- 组件数据交互：
  1. 父子组件数据交互：props+回调函数/props+自定义事件
  2. 跨组件数据交互：Context/provide/inject



###  相同点

- 都有组件化思想
- 都支持服务器端渲染
- 都有Virtual DOM（虚拟dom）
- 数据驱动视图
- 都有支持native的方案：`Vue`的`weex`、`React`的`React native`
- 都有自己的构建工具：`Vue`的`vue-cli`、`React`的`Create React App`

### 区别

- 数据流向的不同。`react`从诞生开始就推崇单向数据流，而`Vue`是双向数据流
- 数据变化的实现原理不同。`react`使用的是不可变数据，而`Vue`使用的是可变的数据
- 组件化通信的不同。`react`中我们通过使用回调函数来进行通信的，而`Vue`中子组件向父组件传递消息有两种方式：事件和回调函数
- diff算法不同。`react`主要使用diff队列保存需要更新哪些DOM，得到patch树，再统一操作批量更新DOM。`Vue` 使用双向指针，边对比，边更新DOM



### TS

```
console.log(String()) // 空字符串

// 'xxx: number' 表示声明一个number类型
const num: number = 123

// 声明一个函数的参数类型(number以及any)和返回值(void)
function fn (arg1: number, arg2: any): void {
    // todo
}
fn(num, [1,2,3,4])

// 声明一个接口
interface IPerson {
    name: string // IPerson需要包含一个name属性，类型是string
    age: number // IPerson需要包含一个age属性，类型是number
    family: string[] //IPerson需要包含一个family属性，类型是数组，数组里面都是string类型的数据
    sex?: '男' | '女' // IPerson可选一个sex属性，值为'男'或者'女'或者undefined
}
// 使用IPerson接口定义一个对象，如果对象不符合IPerson的定义，编译器会飘红报错
const person: IPerson = {
    name: '小王',
    age: 12,
    family: ['爹', '娘'],
}

// type类似interface，以下写法等同用interface声明IPerson
type IPerson2 = {
    name: string
    age: number
    family: string[]
    sex?: '男' | '女'
}
// 因此可以直接定义过来
const person2: IPerson2 = person

```

优势：

1. 自动检查bug
2. 清晰的函数参数、接口属性、class和enum增强
3. ts泛型



缺点：

1. vue2.x不支持
2. 有些报错处理太冗余
