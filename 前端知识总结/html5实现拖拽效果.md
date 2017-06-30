>在此之前，实现拖拽操作都是开发人员自定义逻辑实现的，但是HTML5提供了拖拽API ，使得拖拽操作的实现变得简单。

![fish.gif](http://upload-images.jianshu.io/upload_images/3229842-be565537afb2dae0.gif?imageMogr2/auto-orient/strip)

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>拖拽</title>
    <style>
        #div1 {
            width: 100px;
            height: 100px;
            padding: 200px;
            position: absolute;
            top:100px;
            left:100px;
            background: url("bowl.png") no-repeat;
        }
    </style>
</head>
<body>
![](fish.png)
<div id="div1" ondrop="drop(event)" ondragover="allowDrop(event)">
</div>
<script>
    function drag(ev) {
        ev.dataTransfer.setData("text", ev.target.id);
    }
    function allowDrop(ev) {
        ev.preventDefault();
    }
    function drop(ev) {
        ev.preventDefault();
        var data = ev.dataTransfer.getData("text");
        ev.target.appendChild(document.getElementById(data));
    }
</script>
</body>
</html>
```
##下面分步讲解一下是如何实现拖拽效果的：
---
### 设置元素为可拖放模式
首先，为了使元素可拖动，把`` draggable`` 属性设置为 ``true ``：
```html
<img draggable="true" />
```
### 被拖放物体 - ondragstart
在上面的例子中，``ondragstart ``属性调用了一个函数，``drag(event)``，它规定了被拖动的数据。
``dataTransfer.setData()`` 方法设置被拖数据的数据类型和值：
```
function drag(ev)
{
ev.dataTransfer.setData("text",ev.target.id);
}
```
在这个例子中，数据类型是 ``"text"``，值是可拖动元素的 id为`` ("img1")``。

###放到何处 - ondragover
``ondragover ``事件规定在何处放置被拖动的数据。
默认地，无法将数据/元素放置到其他元素中。如果需要设置允许放置，我们必须阻止对元素的默认处理方式。
这要通过调用 ``ondragover`` 事件的 ``event.preventDefault()`` 方法：
```
event.preventDefault();
```
###进行放置 - ondrop
当放置被拖数据时，会发生 ``drop`` 事件。
在上面的例子中，``ondrop`` 属性调用了一个函数，``drop(event)：``
```javascript
function drop(ev)
{
ev.preventDefault();
var data=ev.dataTransfer.getData("text");
ev.target.appendChild(document.getElementById(data));
}
```
#####代码解析：
* 调用 ``preventDefault() ``来避免浏览器对数据的默认处理（``drop`` 事件的默认行为是以链接形式打开）
* 通过 ``dataTransfer.getData("text") ``方法获得被拖的数据。该方法将返回在 ``setData()`` 方法中设置为相同类型的任何数据。
* 被拖数据是被拖元素的`` id ("img1")``
* 把被拖元素追加到目标元素中,如下图所示，被拖放物体放在目标物体的``content``的左上角

![实例](http://upload-images.jianshu.io/upload_images/3229842-6931f0aa4fbde778.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
