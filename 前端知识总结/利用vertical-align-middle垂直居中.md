````
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>CSS垂直居中</title>
    <style>
        .wrapper{
            width: 500px;
            height: 500px;
            background-color: pink;
            text-align: center;
        }

        .box{
            width: 100px;
            height: 100px;
            background-color: deepskyblue;
            display: inline-block;
            vertical-align: middle;
            margin: 0 auto;
        }
    </style>
</head>
<body>
<div class="wrapper">
    <div class="box"></div>
</div>
</body>
</html>
````

![效果如图所示](http://upload-images.jianshu.io/upload_images/3229842-f4b88e6af61acd2b.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
>以前总是以为vertical-align与text-align是同样的道理，一个是垂直居中，一个是水平居中，结果在这里一点效果也没有。事实上vertical-align与text-align完全不一样，vertical-align不能这样用。

####vertical-align 属性设置元素的垂直对齐方式。该属性定义行内元素的基线相对于该元素所在行的基线的垂直对齐。允许指定负长度值和百分比值。这会使元素降低而不是升高。在表单元格中，这个属性会设置单元格框中的单元格内容的对齐方式。

>第一种用法，先看后面一句“在表单元格中，这个属性会设置单元格框中的单元格内容的对齐方式。”这很容易理解，如果给一个表格的td加一个vertical-align:middle的样式，表格里面的内容会垂直居中，同样的如果给一个vertical-align:bottom就会底部对齐，如果给一个vertical-align:top就会顶部对齐。


>第二种用法，该属性定义行内元素的基线相对于该元素所在行的基线的垂直对齐。假设有两个行内元素a和b，a和b都是div，当a加了一个vertical-align:middle样式之后，b的底部（基线）就会对齐a的中间位置，如下图：

![图示](http://upload-images.jianshu.io/upload_images/3229842-5c86bf97eef51728.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

>如果a和b都加了一个vertical-align:middle样式，那么就互相对齐了对方的中间位置，也就是它们在垂直方向上的中线对齐了，如下图：

![图示](http://upload-images.jianshu.io/upload_images/3229842-d205321844c529a4.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

>现在我要让class="box"的div在class="wrapper"的div里面垂直居中，我可以在class="wrapper"的div里面加一个div空标签，把它的高度设为100%，宽度设置为0，再给它一个vertical-align:middle样式，同样的给class="box"的div一个vertical-align:middle样式，那么box就可以在div里面垂直居中了。

````
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>CSS垂直居中</title>
    <style>
        .wrapper{
            width: 500px;
            height: 500px;
            background-color: pink;

            text-align: center;
        }

        .box{
            width: 100px;
            height: 100px;
            background-color: deepskyblue;

            display: inline-block;
            vertical-align: middle;
            margin: 0 auto;
        }

        .help{
        width: 0;
        height: 100%;
        display: inline-block;
        vertical-align: middle;
        }
    </style>
</head>
<body>
<div class="wrapper">
    <div class="box"></div>
    <div class="help"></div>
</div>
</body>
</html>
````

![图示](http://upload-images.jianshu.io/upload_images/3229842-ae649e6ff036dd75.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


##下面我们来看一张图来更好理解垂直对齐主要属性值的表现形式

![垂直对齐主要属性值的表现形式.png](http://upload-images.jianshu.io/upload_images/3229842-bd636d582f21a29b.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
