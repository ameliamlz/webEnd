## html相关

1. 基础

   em和i：都表示斜体，但em是语义化标签，i是纯样式标签

2. **html5**

   - **语义化标签**：语义化意味着顾名思义，HTML5的语义化指的是合理正确的使用语义化的标签来创建页面结构，如  header,footer,nav，从标签上即可以直观的知道这个标签的作用，而不是滥用div。 语义化的优点有: 代码结构清晰，易于阅读，利于开发和维护 方便其他设备解析（如屏幕阅读器）根据语义渲染网页。 有利于搜索**引擎优化**（SEO），搜索引擎爬虫会根据不同的标签来赋予不同的权重
   - **增强型(智能)表单**：HTML5 拥有多个新的表单 Input 输入类型。这些新特性提供了更好的输入控制和验证。表单属性：<datalist>/<keygen>/placeholder/autofocus/
   - **视频和音频**：HTML5 提供了播放音频文件的标准，即使用 <audio> 元素。<video>:autoplay/controls/loop/width/height
   - canvas绘图：标签只是图形容器，必须使用脚本来绘制图形。
   - svg绘图
   - 地理定位：HTML5 Geolocation（地理定位）用于定位用户的位置。
   - 拖放API：拖放是一种常见的特性，即抓取对象以后拖到另一个位置。在 HTML5 中，拖放是标准的一部分，任何元素都能够拖放。
   - webworker
   - WebStorage
   - WebSocket：WebSocket是HTML5开始提供的一种在单个 TCP 连接上进行全双工通讯的协议。

   /<header>/<nav>/<aside>/<section>/<main>/<footer>/

3. **DOM操作**

   - 获取元素：document.querySelector()/document.querySelectorAll()
   - 类名操作：Node.classList.add/remove/toggle(有则移除，无则添加)/contains('class')

4. 获取网页被卷去的高度

   - document.body.scrollTop
   - document.documentElement.scrollTop

   注：两者只能有一个在访问

5. 前端性能优化

   - 选择服务端渲染
   - CDN
   - 将CSS放头部，JavaScript放尾部
   - 减少回流和重绘的操作
   - 浏览器缓存 
   - 防抖、节流
   - 资源懒加载、预加载
   - 开启Nginx gzip压缩，服务端压缩，webpack压缩(js/css/html)，http2首部压缩
   - 使用flex布局

6. 前端模块化

   概念：将一个复杂的程序按一定规范封装成几个块，只暴露一些接口。

   进化过程：全局函数-namespace模式-IIFE模式

   好处：避免命名冲突；更好的分离，按需加载；更高的复用性；

   问题来了，引入多个<script>后出现的问题：

   - 请求过多
   - 依赖模糊
   - 难以维护

   模块化规范：

   1. CommonJS：每个文件就是一个作用域，运行时确认模块的依赖关系

   2. ES6模块化：export，输出值的引用

      **① CommonJS 模块输出的是一个值的拷贝，ES6 模块输出的是值的引用**。

      **② CommonJS 模块是运行时加载，ES6 模块是编译时输出接口**。

   3. AMD：待补充

   4. CMD：待补充

7. 前端工程化

   开发—测试—部署

   - 统一规范：代码，git，项目，ui
   - 测试
   - 部署
   - 监控
   - 性能优化
   
8. **websocket**

   WebSocket的出现，使得**浏览器**具备了**实时双向通信**的能力。HTML5开始提供的一种浏览器与服务器进行**全双工通讯**的网络技术，属于应用层协议。它基于TCP传输协议，并复用HTTP的握手通道。

   相对http的优点：

   1. 支持双向通信，实时性更强。
   2. 更好的二进制支持。
   3. 较少的控制开销。连接创建后，websocket客户端、服务端进行数据交换时，协议控制的数据包头部较小。在不包含头部的情况下，服务端到客户端的包头只有2~10字节（取决于数据包长度），客户端到服务端的的话，需要加上额外的4字节的掩码。而HTTP协议每次通信都需要携带完整的头部。
   4. 支持扩展。websocket协议定义了扩展，用户可以扩展协议，或者实现自定义的子协议。（比如支持自定义压缩算法等）

   工作原理：

   1. 如何建立连接：协议升级(复用了http通道)
   2. 如何交换数据
   3. 数据帧格式：首部字段减少+掩码算法
   4. 如何维持连接：连接保持+心跳(因为要一直保持)

