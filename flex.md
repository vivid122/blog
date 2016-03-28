#Flex总结
*2016.03.28*

flexbox是w3c在09年为了解决较为复杂的web界面的布局方式而定义的标准，目前较新版本的浏览器支持。（IE10+,Firefox22+，Chrome21+，Safari7/7.1+，Opera29+）
###flexbox是一种布局模块而不是单一的属性。
flex布局依赖于flex directions，包含包含父元素(flex container)和子元素(flex items)的属性。
模块主要组成：父元素（容器 flex container），子元素（flex items）。主轴，主轴方向（沿容器的主轴配置伸缩项目，主轴向主轴方向延伸，从主轴起点边开始到终点边结束）侧轴（与主轴垂直的轴）。

###flex属性
**1.display（flex container）**
>flex  ||  inline-flex

一般容器用flex，行内元素用inline-flex。
不过，设为Flex布局以后，子元素的`float、clear`和`vertical-align`属性将失效。

**2.flex-derection(flex container)**
>row | row-reverse | column | column-reverse

- row 默认值  主轴为水平方向，起点在左端。
- row-reverse：主轴为水平方向，起点在右端。
- column：主轴为垂直方向，起点在上沿。
- column-reverse：主轴为垂直方向，起点在下沿。

**3. flex-wrap（flex container）**
> nowrap | wrap | wrap-reverse 

默认情况下，项目都排在轴线上。flex-wrap属性定义一条轴线排不下时如何换行。


- nowrap(默认值）：默认不换行。
- wrap 换行，第一行在上方。
- wrap-reverse 换行，第一行在下方。


**4.flex-flow（flex container）**
这个是“flex-direction”和“flex-wrap”属性的缩写版本。同时定义了伸缩容器的主轴和侧轴。其默认值为`row nowrap`。
><flex-direction> | <flex-wrap>
#####flex可以实现水平垂直居中
在Flex容器中，当项目边距设置为“auto”时，设置自动的垂直边距将使该项目完全集中两个轴。

**5.justify-content（flex container）**

>flex-start | flex-end | center | space-between | space-around;

- flex-start(默认值)：左对齐
- flex-end：右对齐
- center：向一行的中间位置靠齐。
- space-between：两端对齐，中间间隔相等
- space-around：每个项目两侧的间隔相等。项目之间的间隔比项目与边框的间隔大一倍
![](http://img.blog.csdn.net/20150616151746589)


**6.align-content（flex container）**
>flex-start | flex-end | center | space-between | space-around | stretch;


- flex-start：交叉轴的起点对齐。
- flex-end：交叉轴的终点对齐。
- center：交叉轴的中点对齐。
- baseline: 项目的第一行文字的基线对齐。
- stretch（默认值）：如果项目未设置高度或设为auto，将占满整个容器的高度。


![](http://img.blog.csdn.net/20150616163037523)
定义了多根轴线的对齐方式

**7.align-items（flex container）**
>flex-start | flex-end | center | baseline | stretch



- stretch(默认值)：如果项目未设置高度或设为auto，将占满整个容器的高度。
- flex-start：交叉轴的起点对齐。
- flex-end：交叉轴的终点对齐。
- center：交叉轴的中点对齐。
- baseline: 项目的第一行文字的基线对齐。
![](http://img.blog.csdn.net/20150616152600533)

####项目属性
**1.align-self（flex items）**
>auto | flex-start | flex-end | center | baseline | stretch;

用来在单独的伸缩项目上覆写默认的对齐方式

**2.flex-grow（flex items）**
属性定义项目的放大比例，默认为0，即如果存在剩余空间，也不放大。

**3.flex-shrink(flex items)**
属性定义了项目的缩小比例，默认为1，即如果空间不足，该项目将缩小。
如果所有项目的flex-shrink属性都为1，当空间不足时，都将等比例缩小。如果一个项目的flex-shrink属性为0，其他项目都为1，则空间不足时，前者不缩小。
负值对该属性无效。

**4.flex-basis(flex items)**
flex-basis属性定义了在分配多余空间之前，项目占据的主轴空间（main size）。浏览器根据这个属性，计算主轴是否有多余空间。它的默认值为auto，即项目的本来大小。

**5.flex（flex items)**
flex属性是flex-grow, flex-shrink 和 flex-basis的简写，默认值为0 1 auto。后两个属性可选。
该属性有两个快捷值：auto (1 1 auto) 和 none (0 0 auto)。
建议优先使用这个属性，而不是单独写三个分离的属性，因为浏览器会推算相关值

**6.order(flex items）**
order属性定义项目的排列顺序。数值越小，排列越靠前，默认为0。
   
  
  
  
  
  
 

*参考：*

[segmentfault](https://segmentfault.com/a/1190000002910324)

[阮一峰博客](http://www.ruanyifeng.com/blog/2015/07/flex-grammar.html?utm_source=tuicool)

[Using CSS flexible boxes](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Flexible_Box_Layout/Using_CSS_flexible_boxes)