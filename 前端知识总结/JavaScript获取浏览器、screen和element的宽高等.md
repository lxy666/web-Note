# window
## 1、
>## window.innerWidth/innerHeight:  
浏览器可见区域的内宽度、高度（不含浏览器的边框，但包含滚动条）。

``
对于Internet Explorer、Chrome、Firefox、Opera 以及 Safari：
window.innerHeight - 浏览器窗口的内部高度
window.innerWidth - 浏览器窗口的内部宽度
对于 Internet Explorer 8、7、6、5：
document.documentElement.clientHeight
document.documentElement.clientWidth
或者
document.body.clientHeight
document.body.clientWidth
``
## 2、
>## window.outerWidth/outerHeight：
浏览器外宽度（包含浏览器的边框，因各个浏览器的边框边一样，得到的值也是不一样的）。
``
兼容：ie9/10、chrome、firefox。
``

### 注意：没有window.width属性。
## 3、
>## window.screenLeft/screenTop:  
浏览器的位移
ie浏览器的内边缘距离屏幕边缘的距离。
chrome浏览器的外边缘距离屏幕边缘的距离。
``
兼容：ie6/7/8/9/10、chrome。
``

## 4、
>## window.screenX/screenY:  
浏览器的位移
浏览器的外边缘距离屏幕边缘的距离。
chrome浏览器的外边缘距离屏幕边缘的距离。
``
兼容：ie9/10、chrome、firefox。
chrome的screenLeft和screenX是相等的（其目的是为了兼容ie和firefox，两个属性都兼备了，但更趋向于firefox，chrome的这种做法不止这一处，还有很多，其实这种做法便于开发者移植，但对开发者的开发过程产生了一定的混淆），ie9/10的screenLeft是大于screenX的。
``

## 5、
>## window.pageXOffset/pageYOffset
表示浏览器X轴（水平）、Y轴（垂直）滚动条的偏移距离。
``
兼容：ie9/10、chrome、firefox。
``

## 6、
>## window.scrollX/scrollY
表示浏览器X轴（水平）、Y轴（垂直）滚动条的偏移距离。由此可知，在chrome和firefox中window.pageXOffset和window.scrollX是相等的.
``
兼容：chrome、firefox。
``

# screen
## 1、
>## screen.width/height
屏幕的宽度、高度（指的是屏幕的分辨率，单位为像素）。
``
兼容：ie6/7/8/9/10、chrome、firefox。
``

## 2、
>## screen.availWidth/availHeight
屏幕的可用宽度、高度（通常与屏幕的宽度、高度一致）。
``
兼容：ie6/7/8/9/10、chrome、firefox。
``

# element
## 1、
>## elment.clientWidth/clientHeight
有滚动条时：clientWidth=元素左内边距宽度+元素宽度+元素右内边距宽度-元素垂直滚动条宽度
无滚动条时：clientWidth=元素左内边距宽度+元素宽度+元素右内边距宽度

#### 使用该特性可以计算出的滚动条宽度（即设置元素的内容宽度超过元素宽度，然后分别设置是否超过隐藏，两次的clientWidth差值就是滚动条的宽度）。
``
兼容：chrome、firefox、ie6/7/8/9/10。
``

## 2、
>## element.clientLeft/clientTop
clientLeft为左边框宽度，clientTop为上边框宽度。
``
兼容：chrome、firefox、ie6/7/8/9/10。·
``

## 3、
>## element.offsetWidth/offsetHeight
offsetWidth=元素左边框宽度+元素左内边距宽度+元素宽度+元素右内边距宽度+元素右边框宽度。
``
兼容：chrome、firefox、ie6/7/8/9/10。
``

## 4、
>## element.offsetLeft/offsetTop
表示该元素相对于最近的定位祖先元素的距离，
chrome：offsetLeft=定位祖先左边框宽度+定位祖先元素左内边距宽度+左位移+左外边距宽度
ie6/7/8/9/10、firefox：offsetLeft=定位祖先元素左内边距宽度+左位移+左外边距宽度。
chrome比其他浏览器多计算了定位祖先元素的边框。offsetTop同理。
``
兼容：chrome、firefox、ie6/7/8/9/10。
``

## 5、
>## element.scrollWidth/scrollHeight
有滚动条时：chrome、firefox、ie8/9/10：左内边距宽度+内容宽度。
ie6/7：左内边距宽度+内容宽度+右内边距宽度（是由CSS的BUG引起）。
无滚动条时：左内边距宽度+宽度+右内边距宽度。
``
兼容：chrome、firefox、ie8/9/10、ie6/7（半兼容）。
``

## 6、
>## element.scrollLeft/scrollTop
获得水平、垂直滚动条的距离。
``
兼容：chrome、firefox、ie6/7/8/9/10。
``

# 事件属性
## 1、
>## clientX、clientY
clientX 事件属性返回当事件被触发时鼠标指针向对于浏览器页面（或客户区）的水平坐标。
clientY 事件属性返回当事件被触发时鼠标指针向对于浏览器页面（或客户区）的垂直坐标。
客户区指的是当前窗口。

语法
```
event.clientX;
event.clientY;
```
## 2、
>## event.pageX、event.pageY
类似于event.clientX、event.clientY，但它们使用的是文档坐标而非窗口坐标。这2个属性不是标准属性，但得到了广泛支持。IE事件中没有这2个属性。

## 3、
>## event.offsetX、event.offsetY
鼠标相对于事件源元素（srcElement）的X,Y坐标，只有IE事件有这2个属性，标准事件没有对应的属性。

## 4、
>## event.screenX、event.screenY
鼠标相对于用户显示器屏幕左上角的X,Y坐标。标准事件和IE事件都定义了这2个属性


# 总结
>屏幕宽度：window.screen.width。·
浏览器内宽度：window.innerWidth || document.documentElement.clientWidth。
元素内容宽度：element.clientWidth。
元素占位宽度：element.offsetWidth。
