# css的相对定位
>对一个元素进行相对定位，它将出现在它所在的位置，然后通过水平或垂直方向的设置，它会相对于它原来的位置进行移动。

#### 例如：
````

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>relative</title>
    <style>
        #box1{
            display: inline-block;
            height: 100px;
            width: 100px;
            border: 1px solid red;
        }
        #box2{
            display: inline-block;
            height:100px;
            width:100px;
            border: 1px solid yellow;
        }
        #box3{
            display: inline-block;
            height: 100px;
            width: 100px;
            border: 1px solid blue;
        }
    </style>
</head>
<body>
    <div id="box1">box1</div>
    <div id="box2">box2</div>
    <div id="box3">box3</div>
</body>
</html>

````
![移动前的位置.png](http://upload-images.jianshu.io/upload_images/3229842-0ebf17d25bcd6a24.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

#### 相对定位下box2的位置
````

#box2{
            display: inline-block;
            height:100px;
            width:100px;
            border: 1px solid yellow;
            position: relative;
            top :40px;
            left: 40px;
        }

````        
![相对定位.png](http://upload-images.jianshu.io/upload_images/3229842-18c9c3498d23942d.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

>#### 将 top 设置为 40像素，那么框在原位置顶部下面 40 像素的地方。将left 设置为 40 像素，那么框会在原位置左边40像素的位置，也就是将元素向右下方移动。

# css的绝对定位
>css的相对定位，是使元素脱离文档流，不再占据位置，绝对定位的元素的位置相对于最近的已定位祖先元素，如果元素没有已定位的祖先元素，那么它的位置相对于最初的包含块。

#### 对box2进行相对定位 
````

#box2{
            display: inline-block;
            height:100px;
            width:100px;
            border: 1px solid yellow;
            position: absolute;
            top :40px;
            left: 40px;
        }

````
![绝对定位.png](http://upload-images.jianshu.io/upload_images/3229842-dbd318832e65d089.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

>#### 将box2的 top 设置为 40px，left 设置为 40 px，此元素无祖先元素，它的位置相对于最初的包含块向下40px，向右40px。效果如上图所示。
