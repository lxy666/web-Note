####WEB Application与Native Application的区别
-------
| WEB Application |  Native Application|
| --- | --- |
|运行在服务器上|通过App Store下载|
|通过浏览器执行|直接运行在移动设备上|
| 使用的前端技术| 使用的技术 |
| html,css,Javascript |Objective-C(ios),Java(Android)  |
####Web Apps发布在服务器上
-------
*  #####使用Dropbox发布自己的Web Apps
Dropbox 在国外是一款非常火的云存储的软件，提供免费和收费服务，在不同操作系统下有客户端软件，并且有网页客户端，使用这个软件发布自己的Web Apps的原因是，它天然的集成了发布一个静态网站的功能。
* #####Dropbox的限制
######-静态网站
  没有数据库的支持，也没有php、Java、asp服务端的程序来支持的的网站，主要的由html、CSS、JavaScript语言构成。
######-速度较慢
 Dropbox主服务器在国外。
######-域名不宜记忆 
域名长，存在不便记忆的参数。
* #####步骤
1.登录www.dropbox.com，若没有账号需要注册一个。
2.下载与电脑相应版本的Dropbox。
3.安装Dropbox。
4.将工程粘贴到刚刚下载的Dropbox云存储空间的public内。
``
由于这是一款较为成熟的软件，所以不需要进行任何配置。如果大家购买服务器的话，就需要进行一系列的配置了。
``
* #####访问发布的Web Apps
对需要用户访问的文件(一般是index.html)点击右键，有一个选项是复制公共链接，点击后会有一个url复制到剪切板上，这个是由Dropbox自动生成的url，用浏览器打开这个链接即可访问。
-------
####Web Application的优点
>*  对于一些简单的应用程序，用户无法分清是否为Web Application还是Native Application
* 更容易自适应屏幕
* 更多的硬件支持api在逐渐成熟
* html5 正在逐渐成熟
* 与设备无关，一次开发，多平台使用
* 不局限于App Store

####Native Application的优点
>* 消息通知
* 直接操作设备硬件
* 直接读取设备文件
* 比web具有更流畅细腻的图形渲染效果
* 应用内购买
* 更多的应用内广告嵌入支持

####Hybrid App混合模式的移动应用
>* 介于web-app、Native-app两者之间
* 兼具“Native app的良好用户交互体验”和“web app跨平台开发”的优势

####Web App转换为 Native App
>* PhoneGap
