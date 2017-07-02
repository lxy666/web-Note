## margin 塌陷问题
>在标准文档流中，块级标签之间竖直方向的margin会以大的为准，这就是margin的塌陷现象。

### 1、  两个盒子嵌套关系
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <style>
        *{
            margin: 0;
            padding: 0;
        }
        .box1{
            width: 200px;
            height: 200px;
            background-color: aqua;
        }
        .box2{
            width: 100px;
            height: 100px;
            background-color: pink;
            margin-top: 10px;
        }
    </style>
</head>
<body>
<div class="box1">
    <div class="box2"></div>
</div>
</body>
</html>
```

![运行结果](http://upload-images.jianshu.io/upload_images/3229842-3c737500386feb62.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

>子盒子和父盒子之间没有出现10px的间距，而是父盒子与子盒子一起与页面顶端产生了10px间隙。
#### 解决方法：
方法一：为box1（即父盒子）添加边框
```css
border: 1px solid #ffffff;
```
方法二：为box1（即父盒子）添加overflow属性
```css
overflow: hidden;
```
方法一会产生 1px的边框的距离，方法二不会有影响。



![解决后的效果图](http://upload-images.jianshu.io/upload_images/3229842-b44a6b231711076f.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

### 2、  两个盒子垂直并列
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <style>
        *{
            margin: 0;
            padding: 0;
        }
        .box1{
            width: 100px;
            height: 100px;
            background-color: aqua;
            margin-bottom: 50px;
        }
        .box2{
            width: 100px;
            height: 100px;
            background-color: pink;
            margin-top: 10px;
        }
    </style>
</head>
<body>
<div class="box1"></div>
<div class="box2"></div>
</body>
</html>
```


![运行结果](http://upload-images.jianshu.io/upload_images/3229842-846efbbba7413672.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

>上面的盒子设置 margin-bottom: 50px; 下面的盒子设置 margin-top: 10px；按理说，两个盒子之间的距离应为60px，然而并不是，两盒子之间的距离仅是50px，也就是说两盒子之间的margin出现了重叠部分，故而我们可以得出：垂直之间塌陷的原则是以两盒子最大的外边距为准。这种情况下，可以设置一个外边距。
