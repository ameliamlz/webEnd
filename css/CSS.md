## CSS经典面试题

1. 块级元素和行内元素

   块级元素：address/div/h1-6/p/table/ul

   行内元素：a/br/b/img/span/

2. 标准盒子和IE盒子

   - 标准盒子：width = content	box-sizing: content-box
   - IE盒子：width = border + padding + content    box-sizing: border-box

3. @important和link引入样式的区别

   - 从属关系：只是导入样式表/是html标签，不但能加载css，且能定义rel等属性
   - 加载顺序：页面加载完毕再加载/和页面同时加载
   - 兼容性：css2.1/本身就属于网页标签
   - 权重区别：和位置有关，注意加载和渲染的不同对此造成的影响

4. CSS选择器

   !important>内联>id选择器>类选择器=属性选择器(type=radio)=伪类选择器hover/nth-child>标签选择器(h1)=伪元素选择器(::before)>继承>通配符

   通配选择符、关系选择符(+ > ~)和否定伪类对优先级无影响

   **组合选择器**：

   - 后代选择器(以空格   分隔)：一个父元素下的子元素、曾子元素等
   - 子元素选择器(以大于 **>** 号分隔）：一个父元素下的一级子元素
   - 相邻兄弟选择器（以加号 **+** 分隔）：紧密相邻，有同一父元素
   - 普通兄弟选择器（以波浪号 **～** 分隔）：可间隔其它元素，只要是同一级且相邻，则指定元素之后的所有相邻兄弟元素。

5. 层叠上下文 & 层叠等级 & 层叠顺序

   层叠上下文>层叠等级，层叠顺序是规则(如下图)

   ![image-20211031112733787](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20211031112733787.png)

   层叠上下文的触发条件：

   - html中的根元素
   - 普通元素的position为非static且设置了z-index属性
   - css3新特性：
     1. 父元素的display属性值为`flex|inline-flex`，子元素`z-index`属性值不为`auto`的时候，子元素为层叠上下文元素；
     2. 元素的`opacity`属性值不是`1`；
     3. 元素的`transform`属性值不是`none`；
     4. 元素`mix-blend-mode属性值不是`normal`；
     5. 元素的`filter`属性值不是`none`；
     6. 元素的`isolation`属性值是`isolate`；
     7. `will-change`指定的属性值为上面任意一个；
     8. 元素的`-webkit-overflow-scrolling`属性值设置为`touch`

   z-index：auto & z-index：0区别：

   前者不会产生层叠上下文，后者产生层叠上下文

   

6. 属性继承

   字体、字号、颜色等容易被继承，布局、长宽等不被继承

7. CSS3新增伪类

   nth-child/first-of-type/last-of-type/only-child

   

8. **居中布局**

   - 水平居中

     1. 行内元素：text-align:center

        ps：通过display:block/inline-block/flex/inline-flex给行内元素设置宽高

     2. 块级元素：margin: 0 auto

     3. absolute + left:50% + transform: translate(-50%) :元素本身居中

     4. flex + justify-content:center：设置元素的内部元素居中

   - 垂直居中

     1. 单行文本：line-height: height？
     2. 行内块级元素：？
     3. display:flex + align-items:center
     4. absolute + transform
     5. display:table-cell + vertical-align + text-align

   - 水平垂直居中

     1. absolute+left:50% & top:50% + margin-left & margin-top

     2. absolute+ display: inline + left:0 & top:0  & right:0 & bottom:0 + margin: auto

     3. absolute+left&top+ transform: translate(-50%, -50%)

     4. flex+justify-content + align-items

     5. 父：display:grid + 子：margin:auto

     6. 父：display:tabel-cell + vertical-align:middle + text-align: center + 子：display: line-block

        

9. position

   - static(正常文档流)
   - relative(相对自身static)/仍占用空间
   - absolute(参考最近一个不为static的父级元素)/会脱离正常文档流(不占空间)
   - fixed(相对窗口)/会脱离正常文档流(不占空间)
   - sticky(=relative+fixed) 元素根据正常文档流进行定位，然后相对它的最近滚动祖先。当该祖先的`overflow` 是 `hidden`, `scroll`, `auto`, 或 `overlay`时注意事项：父元素不能overflow:auto/hidden; 必须指定top/bottom/left/right; 高度最小值；父元素内生效

10. **CSS3新特性**

   - background-size background-repeat

   - rgba和透明度

   - background-image background-size background-repeat

   - word-wrap

   - text-shadow/box-shadow

   - font-face

   - border-radius /border-image

   - 渐变：linear / radial

   - 字体：任意字体

   - 2D转换：transform/translate/scale/rotate/

   - 3D转换：perspective/matrix3d

   - 过渡属性：**transition**

   - 动画

   - **盒模型**

     

11. flex布局

   注意：设置flex布局后，子元素float/clear/vertical-align属性会失效

   ​	main axis/ cross axis	

   六个容器属性

   - flex-direction: 决定主轴上项目排列的方向
   - flex-wrap: 定义项目超出高度如何换行
   - flex-flow: flex-direction + flex-wrap
   - justify-content：定义项目在主轴上的对齐方式
   - align-items:定义项目在交叉轴上的对齐方式
   - align-content：定义多根轴线的对齐方式

   项目属性：

   - order: integer 定义项目的排序顺序， 数值越大排序越前
   - flex-grow: 定义项目的放大比例
   - flex-shrink：定义项目的缩小比例
   - flex-basis: 定义多余分配空间
   - flex: flex-grow, flex-shrink, flex-basis
   - align-self: 自身的对齐方式

11. 常见的兼容问题

    - chrome中文字体：12px； -webkit-text-size-adjust: none;

12. BFC

    定位方案：

    - 内部的Box会在垂直方向上一个接一个放置。
    - Box垂直方向的距离由margin决定，属于同一个BFC的两个相邻Box的margin会发生重叠。
    - 每个元素的margin box 的左边，与包含块border box的左边相接触。
    - BFC的区域不会与float box重叠。
    - BFC是页面上的一个隔离的独立容器，容器里面的子元素不会影响到外面的元素。
    - 计算BFC的高度时，浮动元素也会参与计算。
    - 文字层不会被浮动层覆盖，环绕于周围

    触发BFC：

    - 根元素，即html
    - float的值不为none（默认）
    - overflow的值不为visible（默认）
    - display：inline-block|table
    - position：absolut|fixed(优先级最高)

13. 浮动和清除浮动

    浮动带来的问题：父元素无法撑开，

    清除浮动：

    - 父级设置高度
    - clear：left；清除某一浮动，适用于和浮动在同一位置
    - 最后一个浮动元素加空div标签，并添加样式：clear:both
    - 利用伪元素，在父级新增类名并增加样式 .clearfix::after{display:block; clear: both}
    - **父级元素添加样式**：overflow值不为visible，其它值效果不一。原理：BFC

15. CSS优化

16. select+option 多选框 / fieldset+legend 特殊表单

16. 实现三角形

    width:0; height:0; solid; transparent

17. display值

    none/inline/block/list-item/inline-block/table/flex/inline-flex

18. display:none & visibility:hidden &opacity:0 区别

    https://segmentfault.com/a/1190000015116392

    - 空间占据：不占位置/占位置/占位置
    - 是否继承：受父元素影响/不受父元素影响/受父元素影响
    - 是否影响其他元素触发事件：不会/不会/会
    - 产生回流or重绘：回流/产生重绘/产生重绘or not
    - transition：无效/效果表现为延迟显示/有效

    display：none 不显示对应的元素，在文档布局中不再分配空间（回流+重绘）
    visibility：hidden 隐藏对应元素，在文档布局中仍保留原来的空间（重绘）

    - CSS3动画和JS动画的区别
      1. css3动画在性能上会好些但控制上不够灵活
      2. js动画控制能力强，预渲染性能不好

19. CSS动画属性

    - animation-name：动画名，对应@keyframes
    - animation-duration：运行时间
    - animation-timing-function：动画速度，linear、ease先快后慢、ease-in/ease-out/ease-in-out
    - animation-delay：延迟
    - animation-iteration-count：自动播放的次数，infinite循环
    - animation-direction：alternate反向播放
    - animation-fill-mode：静止模式/forwards：停留时保留最后一帧/backwards：停止时回到第一帧/both：同时运用forwards和backwards
    - animation-play-state：指定动画播放状态

20. 两栏布局的实现

    - container:overflow:hidden + div1: float:left + div2: margin-left
    - container:display:flex + div1: width:200px + flex: 1
    - container: overflow:hidden + div1:position:absolute width:200px + div2:margin-left:200px;
    - container: display:table + div1:display:table-cell + div2: display:table-cell

21. 三栏布局的实现

    这两种方式都是打乱正常布局流：所以div的分配是left/right/mid

    - float:left&width + float:right& width + mid:margin-left&margin-right(内容会溢出？)
    - 两边absolute布局（left:0 + right:0） + 中间margin

    以下div是正常的左中右布局：

    - flex布局：父：display:flex + 子：左右设置宽度，中间设置width:100%即可 ，check时内容会自适应缩放。
    - grid布局：grid-template-columns: 300px auto 200px;不受check的影响
    - table布局：每一列都设置display: table-cell，设置左右的宽度，中间width:100%,内容超过后会扩大。

22. Q&A

    - 子元素自适应？子元素设置百分比/子元素不设宽高，利用定位来实现自适应；





