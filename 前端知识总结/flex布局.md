##一、Flex布局
>Flex是Flexible Box的缩写，意为"弹性布局盒模型"，用来为盒状模型提供最大的灵活性，给予容器控制内部元素高度和宽度的能力。任何一个容器都可以指定为Flex布局，行内元素也可以使用Flex布局。它得到以下浏览器的支持：


![浏览器.png](http://upload-images.jianshu.io/upload_images/3229842-eaecdbf8f2d1faea.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

``
注意，设为Flex布局以后，子元素的float、clear和vertical-align属性将失效。
其中在webkit内核的浏览器中使用时，必须加上-webkit-前缀。
``
##二、Flex item
>使用flex布局的容器（flex container），它内部的元素自动成为flex项目（flex item）。

容器默认存在两根轴：水平的主轴（main axis）和垂直的交叉轴（cross axis）。主轴的开始位置（与边框的交叉点）叫做main start，结束位置叫做main end；交叉轴的开始位置叫做cross start，结束位置叫做cross end。
flex item默认沿主轴排列。单个项目在主轴方向上占据的空间叫做main size，在交叉轴方向上占据的空间叫做cross size。
##三、容器的属性
>####容器的6个属性
• flex-direction
• flex-wrap
• flex-flow
• justify-content
• align-items
• align-content


#####1、flex-direction
``
决定主轴的方向，即项目的排列方向。
row:主轴为水平方向，项目沿主轴从左至右排列
column：主轴为竖直方向，项目沿主轴从上至下排列
row-reverse：主轴水平，项目从右至左排列，与row反向
column-reverse：主轴竖直，项目从下至上排列，与column反向
``
#####2、flex-wrap
``
默认情况下，项目排列在一条线上，即主轴上，flex-wrap决定，如果排列不下时，是否换行以及换行的方式。
nowrap（默认）：不换行。
wrap：换行，第一行在上方。
wrap-reverse：换行，第一行在下方。
``
#####3、flex-flow
``
flex-flow属性是flex-direction属性和flex-wrap属性的简写形式。如：row wrap|column wrap-reverse等。默认值为row nowrap，即横向排列 不换行。
``
#####4、justify-content
``
决定item在主轴上的对齐方式，可能的值有flex-start（默认），flex-end，center，space-between，space-around。
当主轴沿水平方向时，具体含义为
flex-start：左对齐
flex-end：右对齐
center：居中对齐
space- between：两端对齐
space-around：沿轴线均匀分布
``
#####5、align-items
``
决定了item在交叉轴上的对齐方式，可能的值有flex-start、flex-end、center、baseline、stretch。
当主轴水平时，其具体含义为
flex-start：顶端对齐
flex-end：底部对齐
center：竖直方向上居中对齐
baseline：item第一行文字的底部对齐
stretch：当item未设置高度时，item将和容器等高对齐
``
#####6、align-content
``
该属性定义了当有多根主轴时，即item不止一行时，多行在交叉轴轴上的对齐方式。如果项目只有一根轴线，该属性不起作用。注意当有多行时，定义了align-content后，align-items属性将失效。align-content可能值含义如下（假设主轴为水平方向）：
flex-start：左对齐
flex-end：右对齐
center：居中对齐
space- between：两端对齐
space-around：沿轴线均匀分布
stretch：各行将根据其flex-grow值伸展以充分占据剩余空间
``
##四、flex item的属性
>item的属性在item的style中设置。item六种属性。
• order
• flex-grow
• flex-shrink
• flex-basis
• flex
• align-self

#####1、order
``
order的值是整数，默认为0，整数越小，item排列越靠前。
``
#####2、flex-grow
``
定义了当flex容器有多余空间时，item是否放大。默认值为0，即当有多余空间时也不放大；可能的值为整数，表示不同item的放大比例。
``
#####3、flex-shrink
``
定义了当容器空间不足时，item是否缩小。默认值为1，表示当空间不足时，item自动缩小，其可能的值为整数，表示不同item的缩小比例。flex-grow。
``
#####4、flex-basis
``
属性定义了在分配多余空间之前，项目占据的主轴空间。浏览器根据这个属性，计算主轴是否有多余空间。它的默认值为auto，即项目的本来大小。
``
#####5、flex
``
flex属性是flex-grow、flex-shrink和flex-basis三属性的简写总和。默认值为0 1 auto。后两个属性可选。
``
#####6、align-self
``
align-self属性允许item有自己独特的在交叉轴上的对齐方式，可覆盖align-items属性。默认值为auto，表示继承父元素的align-items属性，如果没有父元素，则等同于stretch。
auto：和父元素align-self的值一致
flex-start：顶端对齐
flex-end：底部对齐
center：竖直方向上居中对齐
baseline：item第一行文字的底部对齐
stretch：当item未设置高度时，item将和容器等高对齐
``

