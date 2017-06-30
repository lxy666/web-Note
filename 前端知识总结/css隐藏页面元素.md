##Opacity
>opacity属性的意思是设置一个元素的透明度。它不是为改变元素的边界框（bounding box）而设计的。这意味着将opacity设为0只能从视觉上隐藏元素。而元素本身依然占据它自己的位置并对网页的布局起作用。它也将响应用户交互。元素和它所有的内容会被读屏软件阅读，就像网页上的其他元素那样。

```html
<!--html代码-->
<div>1</div>
<div class="ohide">2</div>
```
```css
/*CSS代码*/
div {
  padding: 60px;
  width: 60px;
  font-size: 3em;
  background: pink;
  text-align: center;
  margin: 1%;
  display: inline-block;
  float: left;
  cursor: pointer;
  font-family: 'Lato';
}
.ohide {
  opacity: 0;
  transition: all ease 0.8s;
}
.ohide:hover {
  opacity: 1;
}
```

当你的鼠标移到被隐藏的第 2 个的区块上，元素状态平滑地从完全透明过渡到完全不透明。区块也将``cursor``属性设置为了``pointer``，这说明了用户可以与它交互。



![演示](http://upload-images.jianshu.io/upload_images/3229842-953133c86e5fd487.gif?imageMogr2/auto-orient/strip)
##Visibility
>visibility的值设为hidden将隐藏元素。如同opacity属性，被隐藏的元素依然会对我们的网页布局起作用。与opacity唯一不同的是它不会响应任何用户交互。此外，元素在读屏软件中也会被隐藏。

```html
<!--html代码-->
<div>1</div>
<div class="ohide"><p>2</p></div>
```
```css
/*CSS代码*/
div {
  padding: 60px;
  width: 60px;
  font-size: 3em;
  background: pink;
  text-align: center;
  margin: 1%;
  display: inline-block;
  float: left;
  cursor: pointer;
  font-family: 'Lato';
}
.ohide {
  visibility: hidden;
  transition: all ease 0.8s;
}
.ohide:hover {
  visibility: visible;
}
.ohide p {
  visibility: visible;
  margin: 0;
  padding: 0;
}
```
```javascript
//js代码
var oHide = document.querySelector(".ohide");
var oHideP = document.querySelector(".ohide p");
var count = oHideP.innerHTML;
oHide.addEventListener("click", function(){
    count++;
    oHideP.innerHTML = count;
});
```


![演示](http://upload-images.jianshu.io/upload_images/3229842-131dcfd330f6dd2d.gif?imageMogr2/auto-orient/strip)
* 如果一个元素的visibility被设置为hidden，同时想要显示它的某个子孙元素，只要将那个元素的visibility显式设置为visible即可。
* hover 在隐藏元素上，不要 hover 在p标签里的数字上，你会发现你的鼠标光标没有变成手指头的样子。此时，你点击鼠标，你的 click 事件也不会被触发。
* 而在 div 标签里面的 p 标签可以捕获所有的鼠标事件。一旦你的鼠标移动到文字上，<div>本身变得可见并且点击事件也随之生效。

##Display

>display属性设为none确保元素不可见并且连盒模型也不生成。使用这个属性，被隐藏的元素不占据任何空间。display设为none，任何对该元素交互操作都不能生效。此外，读屏软件也不会读到元素的内容。这种方式产生的效果就像元素完全不存在。任何这个元素的子孙元素也会被同时隐藏。为这个元素添加过渡动画是无效的，它的任何不同状态值之间的切换总是会立即生效。
*  不过请注意，通过 DOM 依然可以访问到这个元素。因此你可以通过 DOM 来操作它，就像操作其他的元素。

```html
<!--html代码-->
<div id="o-hover">Hover</div>
<div id="o-hide"><p>0</p></div>
```
```css
/*CSS代码*/
div {
            height: 60px;
            padding: 60px 0;
            width: 180px;
            font-size: 2em;
            line-height: 60px;
            background: pink;
            text-align: center;
            margin: 1%;
            display: block;
            float: left;
            cursor: pointer;
            font-family: 'Lato';
        }
        #o-hide {
            display: none;
            transition: all ease 0.8s;
        }
        #o-hide:hover {
            display: block;
        }
        #o-hide p {
            display: block;
            margin: 0;
            padding: 0;
        }
```
```javascript
//js代码
var count = 0;
    var oHide = document.getElementById("o-hide");
    var oHover = document.getElementById("o-hover");
    oHover.addEventListener("mouseover", function(){
        count++;
        oHide.innerHTML = '<p>' + count + '</p>';
    });
    oHover.addEventListener("click", function(){
        oHide.style.display = "block";
    });
```


![演示](http://upload-images.jianshu.io/upload_images/3229842-e560a1ce2bb52906.gif?imageMogr2/auto-orient/strip)
>* 第二个 div 内有一个 p 元素，它自己的display属性被设置成block，但是它依然不可见。这是visibility:hidden和display:none的另一个不同之处。在前一个例子里，将任何子孙元素visibility显式设置成visible可以让它变得可见，但是在这个例子中，只要祖先元素的display设置为none，子元素就都不可见。
*  将鼠标移到第一个 div 上面几次，然后点击它。这个操作将让第二个 div 显现出来，它其中的数字将是一个大于 0 的数。这是因为，元素即使被这样设置成对用户隐藏，还是可以通过 JavaScript 来进行操作。

##Position

>假设有一个元素你想要与它交互，但是你又不想让它影响你的网页布局，没有合适的属性可以处理这种情况（opacity和visibility影响布局， display不影响布局但又无法直接交互）。在这种情况下，你只能考虑将元素移出可视区域。这个办法既不会影响布局，又能让元素保持可以操作。下面是采用这种办法的 CSS：
```css
.o-hide {
   position: absolute;
   top: -9999px;
   left: -9999px;
}
```
这种方法的主要原理是通过将元素的top和left设置成足够大的负数，使它在屏幕上不可见。采用这个技术的一个好处是用它隐藏的元素的内容可以被读屏软件读取。
