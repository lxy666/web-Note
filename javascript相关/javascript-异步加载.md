>默认情况下javascript是同步加载的，后面的元素要等待javascript加载完毕后才能再次进行加载，对于一些不重要的javascript，如果放在head中会导致网页加载速度变慢。 以下是javascript异步加载的三种方案。


#### 1 .defer
异步加载，但要等到dom文档全部解析完才会被执行。只有IE能用。

```javascript
<script type="text/javascript" defer="defer"> 
//代码区
</script> 
```
#### 2. async： 
异步加载，加载完就执行，async只能加载外部脚本，不能把js写在script 标签里。
```javascript
<script type="text/javascript" src="demo.js" async="async"></script> 
```
###### 注释：有多种执行外部脚本的方法： 
• 如果 async="async"：脚本相对于页面的其余部分异步地执行（当页面继续进行解析时，脚本将被执行） 
• 如果不使用 async 且 defer="defer"：脚本将在页面完成解析时执行 
• 如果既不使用 async 也不使用 defer：在浏览器继续解析页面之前，立即读取并执行脚本 

#### 3.创建script，插入到DOM中，加载完毕后callBack
```javascript
function asyncLoaded(url, callBack) {
        var script = document.createElement('script');
        script.type = 'text/javascript';
        if (script.readystate) {//兼容IE
            script.onreadystatechange = function () {//状态改变触发事件
                if (script.readyState == 'loaded' || script.readyState == 'complete') {
                    callBack();
                    script.onreadystatechange = null;
                }
            }
        } else {
            script.onload = function (e) {
                callBack();
            }
        }
        script.src = url;
        document.body.appendChild(script);
    }
```
