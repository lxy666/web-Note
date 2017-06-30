><canvas>是html5新增的画布元素，为了客户端矢量图形而设计的，它自己没有行为(仅仅是一个画图的容器)，但是定义了一个 API 支持脚本化客户端绘图操作。canvas默认的宽为300px，高为150px，你可以直接在该对象上指定宽度和高度，但是，其大多数功能都可以通过 CanvasRenderingContext2D 对象获得。 这是通过 Canvas 对象的 getContext() 方法并且把直接量字符串 "2d" 作为唯一的参数传递给它而获得的。

````
html代码
//添加canvas标签
<canvas width=500 height=500></canvas>
js代码
// 获得canavs元素
var canvas =document.getElementById('myCanvas');
// 获得canvas上下文对象
var ctx = canvas.getContext('2d');
````

``
Internet Explorer 9+, Firefox, Opera, Chrome 以及 Safari 支持 <canvas> 标签。
注释：Internet Explorer 8 以及更早的版本不支持 <canvas> 标签。
``
### 一、路径绘制

````
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>canvas</title>
    <style>
        #canvas {
            border: 1px solid #000000;
        }
    </style>
</head>
<body>
<canvas id="canvas" height="300" width="300"></canvas>
<script>
    var canvas = document.getElementById('canvas');
    var ctx = canvas.getContext('2d');
    ctx.moveTo(100, 100);//移动到( 100，100)坐标点,作为起点
    ctx.lineTo(200, 100); //从当前点绘制直线到(200，100)(上一个点即为当前点)
    ctx.lineTo(200, 200);
    ctx.stroke();//绘制路径
</script>
</body>
</html>
````

![效果图](http://upload-images.jianshu.io/upload_images/3229842-070aa84bd35e4fe8.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
在上述js代码中加入 ctx.closePath();创建一条从当前点回到起始点的路径。
````
//js代码
var canvas = document.getElementById('canvas');
    var ctx = canvas.getContext('2d');
        ctx.moveTo(100, 100);
        ctx.lineTo(200, 100);
        ctx.lineTo(200, 200);
        ctx.closePath();
        ctx.stroke();
````

![效果图](http://upload-images.jianshu.io/upload_images/3229842-f1fa772173f8b969.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
另外，可以填加 lineWidth 设置线段宽度，fill(),进行填充，默认填充色为黑色。当存在fill()时，代码种无 ctx.closePath()也可以进行填充。
````
   //js代码
    var canvas = document.getElementById('canvas');
    var ctx = canvas.getContext('2d');
    ctx.fillStyle = 'red';
    ctx.moveTo(100, 100);
    ctx.lineTo(200, 100);
    ctx.lineTo(200, 200);
    ctx.closePath();
    ctx.fill();
````

![效果图](http://upload-images.jianshu.io/upload_images/3229842-459990261d707d7c.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

#### 说明
>1.fill和stroke方法都是作用在当前的所有子路径。
2.完成一条路径后要重新开始另一条路径时必须使用beginPath()方法, beginPath开始子路径的一个新的集合。
例如：

````
    var canvas = document.getElementById('canvas');
    var ctx = canvas.getContext('2d');
    ctx.strokeStyle= 'red';
    ctx.moveTo(100, 100);
    ctx.lineTo(200, 100);
    ctx.closePath();
    ctx.stroke();
    ctx.strokeStyle='green';
    ctx.moveTo(100, 200);
    ctx.lineTo(200, 200);
    ctx.stroke();
````

![未添加closePath](http://upload-images.jianshu.io/upload_images/3229842-8a045754b9af4674.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![添加closePath](http://upload-images.jianshu.io/upload_images/3229842-91a16bf6eeec164e.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)



### 二、文本
>绘制实心文本、空心文本。

````
var canvas = document.getElementById('canvas');
    var ctx = canvas.getContext('2d');
    ctx.font = "30px Arial";
    ctx.fillText("Hello World", 10, 50);
    ctx.strokeText("Hello World", 10, 100);
````

![文本](http://upload-images.jianshu.io/upload_images/3229842-46303bf1922fbdd3.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

### 三、矩形

>##### 1、ctx.rect(x, y, dx, dy); 
        x,y在矩形左上点的坐标，dx，dy为矩形的宽高。
        需配合ctx.fill() ctx.stroke()使用
##### 2、ctx.fillRect(x, y, dx, dy);
       效果同
       ctx.rect(x, y, dx, dy);
       ctx.fill();
##### 3、ctx.strokeRect(x, y, dx, dy);
       效果同
       ctx.rect(x, y, dx, dy);
       ctx.stroke();
##### 4、ctx.clearRect(x, y, dx, dy);
       擦除某一区域，x,y为需擦除区域的左上点的坐标，dx，dy宽高。

````
var canvas = document.getElementById('canvas');
    var ctx = canvas.getContext('2d');
    ctx.fillRect(50, 50, 50, 100);
    ctx.strokeRect(200,50,50,100);
    ctx.clearRect(50,50,30,30);
````

![效果图](http://upload-images.jianshu.io/upload_images/3229842-724129ee76b3cc61.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
### 四、弧形
>arc(x, y, r, 起始弧度, 结束弧度,弧形的⽅方向(0或1) )
0顺时针 ，1逆时针
默认为0

![各位置的度数](http://upload-images.jianshu.io/upload_images/3229842-a080832faec42f19.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

````
   var canvas = document.getElementById('canvas');
    var ctx = canvas.getContext('2d');
    ctx.arc(100,100,50,0,Math.PI/180*90);
    ctx.stroke();
````

![顺时针 90度圆弧](http://upload-images.jianshu.io/upload_images/3229842-24ab84714fdebedb.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
````
    var canvas = document.getElementById('canvas');
    var ctx = canvas.getContext('2d');
    ctx.arc(100,100,50,0,Math.PI/180*270);
    ctx.stroke();
````

![顺时针 270度圆弧](http://upload-images.jianshu.io/upload_images/3229842-af5cafa3ee19eced.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
````
    var canvas = document.getElementById('canvas');
    var ctx = canvas.getContext('2d');
    ctx.arc(100,100,50,0,Math.PI/180*90,1);
    ctx.stroke();
````
![逆时针  0-90 圆弧](http://upload-images.jianshu.io/upload_images/3229842-cc742bf39f9352c4.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
### 五、图片填充
>createPattern(image,"repeat|repeat-x|repeat-y|no-repeat")

````
    //html代码
    <canvas id="canvas" width="500" height="500"></canvas>
    <img src="" style="visibility: hidden">
    //js代码
    var canvas = document.getElementById('canvas');
    var ctx = canvas.getContext('2d');
    window.onload = function () {
        var Img = document.getElementsByTagName('img')[0];
        ctx.fillStyle = ctx.createPattern(Img, 'repeat');//设置为重复
        ctx.fillRect(0, 0, 500, 400);//填充范围
    };
````

![效果图](http://upload-images.jianshu.io/upload_images/3229842-345819c436e06b0a.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
### 六、渐变效果
>##### 渐变可以填充在矩形, 圆形, 线条, 文本等等, 各种形状可以自己定义不同的颜色。
###### 以下有两种不同的方式来设置Canvas渐变：
createLinearGradient(x,y,x1,y1) - 线条渐变
x、y为起点坐标，x1、y1为终点坐标
createRadialGradient(x,y,r,x1,y1,r1) -径向渐变
x,y x1,y1为圆点，r、r1位半径
addColorStop()方法指定颜色停止，参数使用坐标来描述，可以是0至1.
使用渐变，设置fillStyle或strokeStyle的值为 渐变，然后绘制形状，如矩形，文本，或一条线。

#### 使用createLinearGradient
````
    var canvas = document.getElementById('canvas');
    var ctx = canvas.getContext('2d');
    var bg = ctx.createLinearGradient(0, 0, 0, 500);
    bg.addColorStop(0, '#000');
    bg.addColorStop(0.5, 'red');
    bg.addColorStop(1, '#fff');
    ctx.fillStyle = bg;
    ctx.fillRect(0, 0, 300, 300);
````
![效果图](http://upload-images.jianshu.io/upload_images/3229842-c0e401433e2225da.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

````
  var canvas = document.getElementById('canvas');
    var ctx = canvas.getContext('2d');
    var gradient_font = ctx.createLinearGradient(0, 0, canvas.width, 0);
    gradient_font.addColorStop(0,'blue');
    gradient_font.addColorStop(0.3,'red');
    gradient_font.addColorStop(0.6,'yellow');
    gradient_font.addColorStop(1,'green');
    ctx.font = '40px Arial';
    ctx.fillStyle = gradient_font;
    ctx.fillText('hello world', 50, 150);
````

![文字渐变效果](http://upload-images.jianshu.io/upload_images/3229842-48245eac32c45ef6.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
#### 使用createRadialGradient
````
    var canvas = document.getElementById('canvas');
    var ctx = canvas.getContext('2d');
    var bg = ctx.createRadialGradient(150, 150, 50, 150, 150, 110);
    bg.addColorStop(0, '#fff');
    bg.addColorStop(0.5, 'pink');
    bg.addColorStop(1, '#fff');
    ctx.fillStyle = bg;
    ctx.fillRect(0, 0, 300, 300);
````


![效果图](http://upload-images.jianshu.io/upload_images/3229842-c5ba9078b69a80dd.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
