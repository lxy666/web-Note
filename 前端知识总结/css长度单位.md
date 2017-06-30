>CSS有两种类型的单位长度：相对和绝对。
相对长度单位指定了一个长度相对于另一个长度的属性。对于不同的设备，相对长度更加适用。
绝对长度单位是一个固定的值，它反应一个真实的物理尺寸。绝对长度单位视输出介质而定，不依赖于环境（显示器、分辨率、操作系统等）。

##相对长度单位
###1、em
``
相对于当前对象内文本的字体尺寸。如当前对行内文本的字体尺寸未被人为设置，则相对于浏览器的默认字体尺寸。任意浏览器的默认字体大小都是16px。em的值并不是固定的；em会继承父级元素的字体大小。
``

````
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>css单位</title>
    <style>
        div {
            font-size: 2em;
        }
    </style>
</head>
<body>
测试文字 body
<div class="div1">
    测试文字 div1
    <div class="div2">
        测试文字 div2
        <div class="div3">
            测试文字 div3
        </div>
    </div>
</div>
</body>
</html>
````

![测试结果](http://upload-images.jianshu.io/upload_images/3229842-be658f8a62dacb8d.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

body的font-size是继承根元素html，html的尺寸是浏览器默认尺寸16px；
div1的font-size=2*16px = 32px;
div2的font-size=2*32px = 64px;
div3的font-size=2*64px = 128px;
如果手动设置div2的font-size为40px，div3的font-size应该为2*40px = 80px。
###2、rem
``
em根据父级元素的大小而变化，但是如果嵌套了多个元素，它的大小就不好计算了，这时出现了rem，与em的区别在于rem是相对于根元素的,因此不受它的父类影响。css3新加属性，chrome/firefox/IE9+支持。
``
````
 /*在em的示例的css代码中添加*/
.div2{
      font-size: 2rem;
  }
````

![测试结果](http://upload-images.jianshu.io/upload_images/3229842-2adc3a9be9858f24.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
###3、vw、vh
``
vh vw全称为Viewport Height和Viewport Width 意思就是视窗 ,vh、vw是相对于视口的高度和宽度。1vh 等于1/100的视口高度，1vw 等于1/100的视口宽度。
``
>比如：浏览器高度900px，宽度为750px, 1 vh =  9 px，1vw = 7.5 px。设置一个和屏幕同宽的标题，h1{font-size:100vw}，那标题的字体大小就会自动根据浏览器的宽度进行缩放，以达到字体和viewport大小同步的效果。

###4、vmin、vmcx
``
vmin：vw和vh中较小的那个。
vmax：vw和vh中较大的那个。
``
>例如，如果浏览器设置为1100px宽、700px高，1vmin会是7px,1vmax为11px。然而，如果宽度设置为800px，高度设置为1080px，1vmin将会等于8px而1vmax将会是10.8px


###5、ex
``
当前字体的x-height(当前字体小写x的高度)，在无法确定x高度的情况下以0.5em计算。
``
###6、ch
``
数字0的宽度，无法确定时为0.5em。
``
###7、%
``
相对于包含它的最近的父元素的高度和宽度而言。
``
###8、px(Pixel)
``
相对于设备的长度单位，像素是相对于显示器屏幕分辨率而言的。Windows用户所使用的分辨率一般是96像素/英寸。而MAC用户所使用的分辨率一般是72像素/英寸。
``
##绝对长度单位
###1、cm
``
厘米
``
###2、mm
``
毫米
``
###3、in(Inch)
``
英寸
``
###4、pt(Point)
``
点，确切的说法是一个专用的印刷单位“磅”，大小为1/72英寸。用于印刷业。
``
###5、pc(Pica)
``
派卡，相当于我国新四号铅字的尺寸。
``
