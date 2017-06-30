# 介绍

>koa是一个相对于express来说，体积更小，更富有表现力的Web框架。koa通过组合不同的generator来避免繁琐的回调函数调用。koa的核心库没有绑定任何的中间件，仅仅提供了一个轻量优雅的函数库，使得编写Web应用变得得心应手。Koa基本上就是一个只有骨架的框架，你可以选择（或者自己写一个）中间件，而不用妥协于Express它们自带的中间件。

### 下面是一段hello world代码 

````
var koa = require('koa');
var controller = require('koa-route');
var app = koa();

app.use(controller.get('/route_test',function*(){
  this.set('Cache-Control','no-cache');
  this.body='hello world!';
}));

app.listen(3000);
````

>其中，
***
koa 是最核心的库。
koa-route 是koa官方开发的“中间件”，用来路由设置。
app 是 koa 生成的 web 服务主程序。
使用 app.use() 注入中间件。
注册一个路由 get 方法 访问根目录下的任何一个文件。
设置为不缓存。
this.body 用于控制输出到页面的内容。
设置监听端口3000。
***

终端开启服务器
访问http://127.0.0.1:3000/route_test


![演示.png](http://upload-images.jianshu.io/upload_images/3229842-d42136a75ab9c54f.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
### 官网依赖模块包括:

>“koa”: ,koa核心模块 
  <br>“koa-route”: 路由模块 
  <br>“koa-static”: 静态文件加载 
  <br>“koa-static-cache”: 静态文件缓存加载 
  <br>“co”:异步流
  <br>“co-fs”: 文件流 
  <br>“co-body”:post JSON模块 
  <br>“co-views”: 视图模块 
  <br>“koa-compose”:函数合并执行 
  <br>“swig”: 模版引擎 
  <br>“xss”:方式xss 攻击 
  <br>“mongoose”:mongo链接库

#### 例子：
````
app.js代码

var koa = require('koa');
var controller = require('koa-route');
var app = koa();
var views = require('co-views');
var render = views('./view/include',{
  map : { html : 'ejs'}
});
app.use(controller.get('/route_test',function*(){
  this.set('Cache-Control','no-cache');
  this.body='hello koa!';
}));
app.use(controller.get('/ejs_test',function*(){
  this.set('Cache-Control','no-cache');
  this.body = yield render('test',{title:'title_test'});
}));
app.listen(3000);
console.log('koa server is started!');

text.html代码

<%=title%> 对title进行html转义
````
> 终端开启服务器
访问http://127.0.0.1:3000/ejs_test'


![结果显示.png](http://upload-images.jianshu.io/upload_images/3229842-17dad69ebc34964f.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

<%=title%> 是对title进行html转义
co-views 是用来渲染模板的库，而 render 是它生成的实例


>#### function *() {}和yield是啥？
这个其实是 Koa 的精髓所在，首先app.use(...)和controller.get(path, ...)传入的参数都是一种写得很像函数的东西，但不同之处是函数的写法是function foo() {...}，而这里的写法多了一个星号，即function *foo() {}。这种写法其实就是 ES6 里的 generator。而yield正是配合这个写法的一种语法。

