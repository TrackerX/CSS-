## 盒模型
1.什么是盒模型：
    是网页CSS布局中的一种思维模型，主要规定了元素是怎么显示的、元素之间的关系。
2.盒模型组成结构：
    由内到外为：content(内容)、padding(内边距)、boder(边框)、margin(外边距)
    特点1：加了padding值后，会把元素原本有的大小撑大，如果让元素原本的大小不变，需要在元素的宽高上减掉所加的padding值。
    特点2：padding属性对背景图片不起作用的，也可以说背景图片的位置不受padding的影响。
    特点3：背景色会延展到padding区域。
3.标准盒模型：
    标准盒模型 的所占位置的组成：宽高（content+padding+border+margin）
    元素宽度实际占有的位置大小： 宽+左右padding+左右border+左右margin
    元素高度实际占有的位置大小： 高+上下padding+上下border+上下margin
4.怪异盒模型：
    盒子的高度 = hight + margin;
    盒子总宽度 = width + margin;
    也就是，width/height 包含了 padding和 border值
5.Box-sizing:
```css
box-sizing: content-box或者border-box或inherit:
```

- content-box 默认值，元素的 width/height 不包含padding，border，与标准盒子模型表现一致
- border-box 元素的 width/height 包含 padding，border，与怪异盒子模型表现一致
- inherit 指定 box-sizing 属性的值，应该从父元素继承



## CSS选择器有哪些？优先级？哪些属性可以继承？

```html
<div id="box">
    <div class="one">
        <p class="one_1">
        </p >
        <p class="one_1">
        </p >
    </div>
    <div class="two"></div>
    <div class="two"></div>
    <div class="two"></div>
</div>
```

**常用的选择器有：**

- id选择器（#box），选择id为box的元素
- 类选择器（.one），选择class为one的元素
- 标签选择器（div），选择标签为div的所有元素
- 后代选择器（#box div），选择id为box元素内部所有的div元素
- 子选择器（.one>one_1），选择父元素为.one的所有.one_1的元素
- 相邻同胞选择器（.one+.two），选择紧接在.one之后的所有.two元素
- 群组选择器（div,p），选择div、p的所有元素

**伪类：**用于已有元素处于某种状态时（滑动、点击等）为其添加对应的样式，这个状态是根据用户行为而动态变化的。常见的有：

```css
:link ：选择未被访问的链接
:visited：选取已被访问的链接
:active：选择活动链接
:hover ：鼠标指针浮动在上面的元素
:focus ：选择具有焦点的
:first-child：父元素的首个子元素
```

**伪元素：**

```css
:first-letter ：用于选取指定选择器的首字母
:first-line ：选取指定选择器的首行
:before : 选择器在被选元素的内容前面插入内容
:after : 选择器在被选元素的内容后面插入内容
```

CSS选择器的优先级：

> **!important > 行内选择器>ID选择器 > 类选择器(包含伪类) > 标签 (包含伪元素)> 通配符 > 继承 > 浏览器默认属性**

优先级算法：每个规则对应一个初始"四位数"：0、0、0、0
　　若是 行内选择符，则加1、0、0、0
　　若是 ID选择符，则加0、1、0、0
　　若是 类选择符/属性选择符/伪类选择符，则分别加0、0、1、0
　　若是 元素选择符/伪元素选择符，则分别加0、0、0、1
然后由左到右比较大小，大的优先级就高，如果相等就就近原则，后面的覆盖前面的



## 说说em/px/rem区别?

从`CSS3`开始，浏览器对计量单位的支持新增了`rem`、`vh`、`vw`、`vm`等一些新的计量单位。

**px：**
px，表示像素，所谓像素就是呈现在我们显示器上的一个个小点，每个像素点都是大小等同的，所以像素为计量单位被分在了绝对长度单位中

**em：**
em是相对长度单位。基准点为父节点字体的大小。如当前对行内文本的字体尺寸未被人为设置，则相对于浏览器的默认字体尺寸（`1em = 16px`）

特点：
- em 的值并不是固定的
- em 会继承父级元素的字体大小
- em 是相对长度单位。相对于当前对象内文本的字体尺寸。如当前对行内文本的字体尺寸未被人为设置，则相对于浏览器的默认字体尺寸
- 任意浏览器的默认字体高都是 16px

**rem：**
rem也是相对单位，相对的只是HTML根元素`font-size`的值

- rem单位可谓集相对大小和绝对大小的优点于一身
- 和em不同的是rem总是相对于根元素，而不像em一样使用级联的方式来计算尺寸

**CSS实现隐藏元素：**

- **display:none**

  特点：元素彻底消失，元素本身占有的空间就会被其他元素占有，会导致重排和重绘，自身绑定的事件不会触发

- **visibility:hidden**

  从页面上仅仅是隐藏该元素，DOM结果均会存在，只是当时在一个不可见的状态，不会触发重排，但是会触发重绘

- **opacity:0**

  设置透明度为0，不会引发重排，一般情况下也会引发重绘。由于其仍然是存在于页面上的，所以他自身的的事件仍然是可以触发的，但被他遮挡的元素是不能触发其事件的。

- **设置height、width模型属性为0**       元素不可见，不占据页面空间，无法响应点击事件

- **position:absolute**     通过定位将元素移到可视范围以外



## BFC

`BFC`（Block Formatting Context），即块级格式化上下文，它是页面中的一块渲染区域，并且有一套属于自己的渲染规则：**具有 BFC 特性的元素可以看作是隔离了的独立容器，容器里面的元素不会在布局上影响到外面的元素，并且 BFC 具有普通容器所没有的一些特性。**

**如何触发BFC：**

- body 根元素
- 浮动元素：float 除 none 以外的值
- 绝对定位元素：position (absolute、fixed)
- display 为 inline-block、table-cells、flex
- overflow 除了 visible 以外的值 (hidden、auto、scroll)

 **BFC 特性及应用**：

1. 同一个 BFC 下外边距会发生折叠
2. BFC 可以包含浮动的元素（清除浮动）
3. BFC 可以阻止元素被浮动元素覆盖



## **元素水平垂直居中的方法有哪些？**

- 利用定位+margin:auto
- 利用定位+margin:负值
- 利用定位+transform
- **table布局**：设置父元素为`display:table-cell`，子元素设置 `display: inline-block`。利用`vertical`和`text-align`可以让所有的行内块级元素水平垂直居中
- **flex布局：**display: flex时，align-items: center表示这些元素将相对于本容器水平居中，justify-content: center也是同样的道理垂直居中
- **grid布局：**  display: grid， align-items:center水平居中，justify-content: center垂直居中

## 说说flexbox（弹性盒布局模型）,以及适用场景？

flex常用属性有：

- flex-direction：决定主轴的方向(即项目的排列方向)
- flex-wrap：弹性元素永远沿主轴排列，那么如果主轴排不下，通过`flex-wrap`决定容器内项目是否可换行
- flex-flow：是`flex-direction`属性和`flex-wrap`属性的简写形式，默认值为`row nowrap`
- justify-content：定义了项目在主轴上的对齐方式
- align-items：定义项目在交叉轴上如何对齐
- align-content：定义了多根轴线的对齐方式。如果项目只有一根轴线，该属性不起作用

## CSS3新增了哪些新特性？

![CSS3新增属性](C:\Users\A\Desktop\面经整理\CSS\图片\CSS3新增属性.JPG)

**新样式：**

边框：border-radius：创建圆角边框；box-shadow：为元素添加阴影

文字：`text-shadow`可向文本应用阴影。能够规定水平阴影、垂直阴影、模糊距离，以及阴影的颜色

css3`新增了新的颜色表示方式`rgba`与`hsla

**transition 过渡：**

```css
transition： CSS属性，持续时间，过度=渡效果(默认ease)，延迟时间(默认0)
```

 **transform 转换**：

`transform`属性允许你旋转，缩放，倾斜或平移给定元素

```
transform-origin`：转换元素的位置（围绕那个点进行转换），默认值为`(x,y,z):(50%,50%,0)
```

使用方式：

- transform: translate(120px, 50%)：位移
- transform: scale(2, 0.5)：缩放
- transform: rotate(0.5turn)：旋转
- transform: skew(30deg, 20deg)：倾斜

**animation 动画：**

animation也有很多的属性

- animation-name：动画名称
- animation-duration：动画持续时间
- animation-timing-function：动画时间函数
- animation-delay：动画延迟时间
- animation-iteration-count：动画执行次数，可以设置为一个整数，也可以设置为infinite，意思是无限循环
- animation-direction：动画执行方向
- animation-paly-state：动画播放状态
- animation-fill-mode：动画填充模式



## 回流和重绘

在HTML中，每个元素都可以理解为一个盒子，会涉及到回流与重绘

- 回流：布局引擎会根据各种样式计算每个盒子在页面上的大小与位置
- 重绘：当计算好盒模型的位置、大小及其他属性后，浏览器根据每个盒子特性进行绘制

具体的浏览器解析渲染机制如下所示：

![img](https://static.vue-js.com/2b56a950-9cdc-11eb-ab90-d9ae814b240d.png)

- 解析HTML，生成DOM树，解析CSS，生成CSSOM树
- 将DOM树和CSSOM树结合，生成渲染树(Render Tree)
- Layout(回流):根据生成的渲染树，进行回流(Layout)，得到节点的几何信息（位置，大小）
- Painting(重绘):根据渲染树以及回流得到的几何信息，得到节点的绝对像素
- Display:将像素发送给GPU，展示在页面上

**回流的触发：**

回流这一阶段主要是计算节点的位置和几何信息，那么当页面布局和几何信息发生变化的时候，就需要回流

**重绘触发时机**：

触发回流一定会触发重绘。另外还有：颜色的修改、文本方向的修改、阴影的修改

**如何减少：**

- 避免使用 `table` 布局，`table` 中每个元素的大小以及内容的改动，都会导致整个 `table` 的重新计算
- 对于那些复杂的动画，对其设置 `position: fixed/absolute`，尽可能地使元素脱离文档流
