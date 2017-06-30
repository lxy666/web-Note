
## 使用Video 元素。
```
<video controls width="500px" id="vid">
    <source src="vid.mp4" />
</video>
```

![图示](http://upload-images.jianshu.io/upload_images/3229842-a8a7617a6e9cb6a6.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

>可以观察到的是video 标签中包含``controls``,添加该标签可以使得播放器工具栏可见。Control bar 和我们平常所见到的一样，非常简单，包含暂停，播放按钮、进度条、最大化、下载，当然了，如果浏览器不同，显示的会不同。

####注意：
* 要确保video 和html 文件存放到同一目录下。如果想放置在不同的目录下，需要设置src 属性。
* HTML5 Video 元素只支持Ogg、MPEG 4、WebM三种格式的视频。

>Ogg = 带有 Theora 视频编码和 Vorbis 音频编码的 Ogg 文件
MPEG4 = 带有 H.264 视频编码和 AAC 音频编码的 MPEG 4 文件
WebM = 带有 VP8 视频编码和 Vorbis 音频编码的 WebM 文件

##使用js控制Video 元素

####设置``video`` 资源`` src``属性。以下不使用``controls`` 属性来设置，使用``js``代码来实现。
```html
<video width="500px" id="vid">
    <source src="vid.mp4" />
</video>
```
####添加play，end 按钮。
```
<input type="button" name="name" value="Play" id="BtnPlay" />
<input type="button" name="name" value="End" id="btnEnd" />
```
#### 创建JS 函数来控制Video播放和暂停。
```
function PlayOrPause() {
        var v = document.getElementById('vid');
        if (v.paused || v.ended) {
            v.play();
            document.getElementById('BtnPlay').value = "Pause";
        }
        else {
            v.pause();
            document.getElementById('BtnPlay').value = "Play";
        }
    }
```
####设置当视频播放完成之后停止播放：
```
function End() {
        var v = document.getElementById('vid');
        v.pause();
        v.currentTime = v.duration;
        document.getElementById('BtnPlay').value = "Play";
    }
```

![video.png](http://upload-images.jianshu.io/upload_images/3229842-616dc15345bd265c.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

##Audio 元素

HTML5使得在页面中加载音频元素变得非常简单。
```
<audio id="audctrl" controls>
    <source src="aud.mp3" type="audio/mp3" />
</audio>
```

![audio元素](http://upload-images.jianshu.io/upload_images/3229842-38bb4f91de6faa73.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
同样可以使用js控制audio 元素，就像控制video元素一样。
