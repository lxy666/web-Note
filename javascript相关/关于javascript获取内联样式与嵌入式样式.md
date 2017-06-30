### 通过style属性设置背景图案
```html
<!--html-->
<div id="change">
change color
</div>
```
```css
/*css*/
#change {
            border: 1px solid black;
            width: 200px;
            height: 200px;
            text-align: center;
            line-height: 200px;
        }
```
```javascript
//js
change.style.backgroundColor="purple";
```

![图示](http://upload-images.jianshu.io/upload_images/3229842-4f2dc1b3e3f95560.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

>在侧边栏设置一个颜色选择器，将``change``的背景颜色设置为选择的颜色，此时颜色选择器的颜色是使用``内联样式``的方式添加的。

![演示.gif](http://upload-images.jianshu.io/upload_images/3229842-e52a11bb97dcdbfd.gif?imageMogr2/auto-orient/strip)
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>css</title>
    <style>
        * {
            margin: 0;
            padding: 0;
        }

        .wrap {
            width: 220px;
            height: 200px;
            position: absolute;
            top: 300px;
            left: -172px;
        }

        .open-close {
            height: 45px;
            width: 48px;
            background: url("open-close.png") no-repeat;
            background-size: contain;
            border: 1px solid grey;
            border-left: none;
            position: absolute;
            top: 0;
            right: 0;
            z-index: 2;
        }

        .changer {
            height: 150px;
            width: 170px;
            position: absolute;
            top: 0;
            left: 0;
            border: 1px solid grey;
            text-align: center;
            padding-top: 8px;
        }

        .list > li {
            display: block;
            width: 36px;
            height: 36px;
            float: left;
            margin-left: 9%;
            margin-top: 10%;
        }

        #change {
            border: 1px solid black;
            width: 200px;
            height: 200px;
            text-align: center;
            line-height: 200px;
        }
    </style>
</head>
<body>
<div class="wrap" id="wrap">
    <!--html-->
    <div class="open-close" id="open"></div>
    <div class="changer">
        <span>颜色选择器</span>
        <ul class="list">
            <li class="color-orange" style="background-color: orange"></li>
            <li class="color-red" style="background-color: red"></li>
            <li class="color-blue" style="background-color: blue"></li>
            <li class="color-black" style="background-color: black"></li>
            <li class="color-green" style="background-color: green"></li>
            <li class="color-pink" style="background-color: pink"></li>
        </ul>
    </div>
</div>
<div id="change">
    change color
</div>
<script>
    var open = document.getElementById("open");
    var wrap = document.getElementById("wrap");
    var list = document.getElementById("list");
    var change = document.getElementById("change");
    var color_change = document.getElementsByTagName("li");
    change.style.backgroundColor = "purple";
    open.onmouseover = function () {
        wrap.style.left = 0 + "px";

    };
    open.onclick = function () {
        wrap.style.left = -172 + "px";
    };
    for (var i = 0; i < color_change.length; i++) {
        color_change[i].id = i;
        color_change[i].onclick = function () {
            change.style.backgroundColor = color_change[this.id].style.backgroundColor;
        }
    }
</script>
</body>
</html>
```
> # 问题：
当颜色选择器的颜色是使用嵌入式或者外部引入的方式添加时，``javascript``的``style``属性无效，获取不到颜色值。
# 解决方法：
>`` javascript``的``style``属性只能获取内联样式，对于外部引入样式和嵌入式样式需要用``currentStyle``属性。但是，``currentStyle``在``Firefox``和``Chrome``下不支持，需要使用如下兼容性代码:
```javascript
HTMLElement.prototype.__defineGetter__("currentStyle", function () {
            return this.ownerDocument.defaultView.getComputedStyle(this, null);
        });
```

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <style>
        * {
            margin: 0;
            padding: 0;
        }
        .wrap {
            width: 220px;
            height: 200px;
            position: absolute;
            top: 300px;
            left: -172px;
        }
        .open-close {
            height: 45px;
            width: 48px;
            background: url("open-close.png") no-repeat;
            background-size: contain;
            border: 1px solid grey;
            border-left: none;
            position: absolute;
            top: 0;
            right: 0;
            z-index: 2;
        }
        .changer {
            height: 150px;
            width: 170px;
            position: absolute;
            top: 0;
            left: 0;
            border: 1px solid grey;
            text-align: center;
            padding-top: 8px;
        }
        .list > li {
            display: block;
            width: 36px;
            height: 36px;
            float: left;
            margin-left: 9%;
            margin-top: 10%;
        }
        .color-orange {
            background-color: orange;
        }
        .color-red {
            background-color: red;
        }
        .color-blue {
            background-color: blue;
        }
        .color-blank {
            background-color: black;
        }
        .color-green {
            background-color: green;
        }
        .color-pink {
            background-color: pink;
        }
        #change {
            border: 1px solid black;
            width: 200px;
            height: 200px;
            text-align: center;
            line-height: 200px;
        }
    </style>
</head>
<body>
<div class="wrap" id="wrap">
    <!--html-->
    <div class="open-close" id="open"></div>
    <div class="changer">
        <span>颜色的选择</span>
        <ul class="list">
            <li class="color-orange"></li>
            <li class="color-red"></li>
            <li class="color-blue"></li>
            <li class="color-blank"></li>
            <li class="color-green"></li>
            <li class="color-pink"></li>
        </ul>
    </div>
</div>
<div id="change">
change color
</div>
<script>
    HTMLElement.prototype.__defineGetter__("currentStyle", function () {
        return this.ownerDocument.defaultView.getComputedStyle(this, null);
    });
    var open = document.getElementById("open");
    var wrap = document.getElementById("wrap");
    var list = document.getElementById("list");
    var change = document.getElementById("change");
    var color_change = document.getElementsByTagName("li");
    change.style.backgroundColor="purple";
    open.onmouseover = function () {
        wrap.style.left = 0 + "px";

    };
    open.onclick = function () {
        wrap.style.left = -172 + "px";
    };

    for (var i = 0; i < color_change.length; i++) {
        color_change[i].id = i;
        color_change[i].onclick = function () {
            change.style.backgroundColor = color_change[this.id].currentStyle.backgroundColor;
        }
    }
</script>
</body>
</html>
```

![演示.gif](http://upload-images.jianshu.io/upload_images/3229842-e52a11bb97dcdbfd.gif?imageMogr2/auto-orient/strip)

