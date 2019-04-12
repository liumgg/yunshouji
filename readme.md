# 要点

## html语义化

- html语义化 用语义化标签定义盒子的作用 语义化标签里加盒子实现功能
- 语义化标签使用
  header nav SEO 对机器更友好
  logo h1 fz0 图片对机器不友好
- 良好的结构分析及构建是界面开发的基石
  header + page
  盒子 装内容 布局方式 网页布局本质是图文混排
  float 传统布局
  flex 新贵
    很好的处理父亲与儿子们的关系，可以不用确定父亲的大小 适合移动端布局
    justify-content:space-between;
    align-item:center;

- 用户体验
  1. Apple UI Guideline 45px
  2. 水平方向上最好不要出现滚动条，overflow: hidden;
  3. 左右不要顶边框，16-18px

## 标准流的默认特性

1. 分行、块级元素，并且能够dispay转换。
2. 块级元素（block）：默认独占一行，不能并列显示，能够设置宽、高，宽度为父盒子的100%。例如：div、p、标题元素（h1-h6）、列表元素（ul li、dl dt dd）
3. 行内元素（inline）：默认并排显示，不能设置宽、高，宽度为内容的宽度。例如：span、a、b、i
4. margin-bottom 和margin-top 塌陷，以最大值为准

## 脱标的元素的特性

- 只要是脱离了标准流，元素都是不区分行、块的，体现在任何元素都可以设置宽、高了。都有了收缩的 性质，就是不设置宽度，就自动缩减为里面内容的宽度。
- 浮动的元素有贴边的性质，绝对定位的元素可以自由定位

## 元素定位-浮动定位

- float语法： float : none | left |right
- 参数值：

1. none : 　对象不浮动
2. left : 　对象浮在左边
3. right : 　对象浮在右边

- 浮动元素的特征有：

1. 块在一排显示；
2. 内联元素支持宽高；
3. 无论是块元素还是内联元素，没有宽度时默认内容撑开宽度；
4. 脱离文档流；
5. 提升层级半级。

- 对其他浮动元素的影响：后浮动的元素永不会超过先浮动元素的顶端。
- 对普通元素的影响：浮动元素会从文档正常流中删除，使得紧挨它的元素位置发生偏移，影响布局。
- 对文字的影响：浮动元素向下延伸时，不会影响正常文本的显示，文本会相对于浮动元素进行偏移。但部分文本背景会被浮动元素遮住。
- 清除浮动指什么? 如何清除浮动?
清除浮动指的是：在非IE浏览器（如Firefox）下，当容器的高度为auto,且容器的内容中有浮动（float为left或right）的元素，在这种情况下，容器的高度不能自动伸长以适应内容的高度，使得内容溢出到容器外面而影响布局的现象，为了防止这个现象的出现而进行的CSS处理，就叫CSS清除浮动

- 注意：某个元素设置了浮动，则同级元素都需要设置浮动。
有高度的父盒子不用清除浮动，否则都需要清除浮动：

1. 使用带clear属性的空元素
在浮动元素后使用一个空元素如`<pre><div class="clear"></div></pre>`，并在CSS中赋予`<pre>.clear{clear:both;}</pre>`属性即可清理浮动。亦可使用`<pre><br class="clear" /></pre>`或`<pre><hr class="clear" /></pre>`来进行清理。
2. 使用CSS的overflow属性
给浮动元素的容器添加overflow:hidden;或overflow:auto;可以清除浮动，另外在 IE6 中还需要触发 hasLayout ，例如为父元素设置容器宽高或设置 zoom:1。
3. 使用CSS的:after伪元素{display:block; overflow:hidden; clear:both; height:0; visibility:hidden; content:".";}

## 元素定位-绝对定位

- position语法： position : static | absolute | relative | fixed
- position参数：

1. static(静态定位): 无特殊定位，对象遵循HTML定位规则
2. absolute(绝对定位): 将对象从文档流中拖出，使用left，right，top，bottom等属性进行绝对定位。而其层叠通过css z-index属性定义。此时对象不具有边距，但仍有补白和边框
3. relative(相对定位): 定位是相对于自身位置定位，元素设置此属性之后仍然处在文档流中，不影响其他元素的布局，但将依据left，right，top，bottom等属性在正常文档流中偏移位置，对象不可层叠
4. fixed(固定定位)：相对于浏览器窗口定位,本质上是一种绝对定位，不为元素预留空间。

- 绝对定位使用通常是父级定义position:relative(通常最好再定义CSS宽度和CSS高度)，子级定义position:absolute属性，并且子级使用left或right和top或bottom进行绝对定位
- 例子
 .父{position:relative} 定义，通常最好再定义CSS宽度和CSS高度
.子{position:absolute;left:10px;top:10px} 这里定义了距离父级左侧距离间距为10px，距离父级上边距离为10px
或
.子{position:absolute;right:10px;bottom:10px} 这里定义了距离父级靠右距离10px,距离父级靠下边距离为10px
- 注意

1. 绝对定位如果父级不使用position:relative，而直接使用position:absolute绝对定位，这个时候使用position:absolute定义的对象无论位于DIV多少层结构，都将会被拖出以`<body>`为父级（参考级）进行绝对定位。
2. 绝对定位与float浮动不能同时使用，如果一起使用，float不会生效