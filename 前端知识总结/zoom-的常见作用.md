* ``zoom``是IE专用属性，firefox等是不支持的。它的本来作用是设置或检索对象的缩放比例，但这作用几乎用不到。 目前非ie由于不支持这个属性，它们又是通过什么属性来实现元素的缩放呢？我们可以通过css3里面的动画属性scale进行缩放。

* 虽然此属性不可继承，但是它会影响对象的所有子对象( children )。这种影响很像 ``background ``和 ``filter ``属性导致的变化。

* 当设置了``zoom``的值之后，所设置的元素就会就会扩大或者缩小，高度宽度就会重新计算了，这里一旦改变``zoom``值时其实也会发生重新渲染，运用这个原理，也就解决了ie下子元素浮动时候父元素不随着自动扩大的问题。

* 通常，当浮动子元素导致父元素塌陷的时候，只要给父元素加上overflow: hidden;来解决，但是对于IE不行，需要触发其hasLayout属性才可以。 

* zoom:1就是IE6 专用的触发 haslayout 属性的。hasLayout是IE特有的一个属性。很多的IE下的css bug都与其息息相关。在IE中,一个元素要么自己对自身的内容进行计算大小和组织，要依赖于父元素来计算尺寸和组织内容。当一个元素的hasLayout属性值为true时，它负责对自己和可能的子孙元素进行尺寸计算和定位。

* hasLayout对于内联元素也可以有效果，当内联元素的hasLayout为true的时候，可以给这个内联元素设定高度和宽度并得到期望的效果。具体关于hasLayout的知识点，可以另外搜索。

###### 通常，在给低版本的IE做兼容的时候会用到zoom:1。例如，清除浮动的时候，我们会这样写：

```css
.clearfix::after {
            content: ".";
            clear: both;
            display: block;
            visibility: hidden;
            overflow: hidden;
            height: 0;
            *zoom: 1;
        }
```
>为了防止低版本的IE浏览器不支持after选择器或者某些属性，在最后加上zoom:1来清除浮动。

 ###### 为了实现inline-block的兼容的时候，我们会这么写：
```css
{
  display: inline-block;
  *display:inline;
  *zoom:1;
｝

```
>因为在IE6、IE7下，只有设置在默认显示方式为inline的元素上才会生效。前面说过，当内联元素的hasLayout为true的时候，可以给这个内联元素设定高度和宽度并得到期望的效果，所以这样做可以达到兼容inline-block的效果。
<br>
这里还要补充一点，为什么 ``*display:inline;*zoom:1;`` 前面有 ``*`` ， ``*`` 放在css属性前面，表示这个属性仅仅应用到 ``Internet Explorer 7`` 以及以下版本。因为 ``Internet Explorer 7 `` 以及以下承认非字母数字（除了下划线）前缀的属性。所以这里，IE7以上的版本作用的是 ``display: inline-block;`` 而在IE7及以下的版本中作用的是 ``display:inline;zoom:1`` 。
