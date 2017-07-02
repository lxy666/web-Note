>vue.js是轻量级的前端框架，2016.10 发布了最新2.0 版本，具有更强大，更快速的特点，使Vue.js 的应用变得更加广泛。

## vue.js 的特点
*  轻量级
* 高效率
* 上手快
* 简单易学
* 文档全面而简洁

## vue.js 的功能
以下是三点功能：
* 模板渲染、数据渲染、数据同步
##### 例子：
```html
<div id="app">
  {{message}}
</div>
```
```javascript
//vuejs实例对象
new Vue({
  el:'#app',                     //对象装载的位置
  data:{                         //数据
    massage:'Hello Vue!'
    }
})
```
![显示](http://upload-images.jianshu.io/upload_images/3229842-00e5bceb8fa05117.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

* 模块化、组件化
##### 例子：
```html
<div id="example">
    <my-component></my-component>
</div>
```
```javascript
// 注册
Vue.component('my-component', { 
    template: '<div>A custom component!</div>'  
})
// 创建根实例
new Vue({
    el: '#example'
})
```
渲染为：
```
<div id="example">
    <div>A custom component!</div>
</div>
```

![显示](http://upload-images.jianshu.io/upload_images/3229842-5a2909212f951c5c.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

##### 组件局部注册

>不必在全局注册每个组件。通过使用组件实例选项注册，可以使组件仅在另一个实例/组件的作用域中可用：

```javascript
var Child = {
  template: '<div>A custom component!</div>'
}
new Vue({
  // ...
  components: {
    // <my-component> 将只在父模板可用
    'my-component': Child
  }
})
```
##### data 必须是函数

使用组件时，大多数选项可以被传入到 Vue 构造器中，有一个例外： data 必须是函数。 实际上，如果你这么做：
```
Vue.component('my-component', {
  template: '<span>{{ message }}</span>',
  data: {
    message: 'hello'
  }
})
```
那么 Vue 会在控制台发出警告，告诉你在组件中 data 必须是一个函数。下面我们就来理解一下这种规则的存在意义。
```
<div id="example-2">
  <simple-counter></simple-counter>
  <simple-counter></simple-counter>
  <simple-counter></simple-counter>
</div>
var data = { counter: 0 }
Vue.component('simple-counter', {
  template: '<button v-on:click="counter += 1">{{ counter }}</button>',
  // data 是一个函数，因此 Vue 不会警告，
  // 但是我们为每一个组件返回了同一个对象引用
  data: function () {
    return data
  }
})
new Vue({
  el: '#example-2'
})
```
由于这三个组件共享了同一个 data ， 因此增加一个 counter 会影响所有组件！我们可以通过为每个组件返回新的 data 对象来解决这个问题，避免直接的引用赋值：
```
data: function () {
  return {
    counter: 0
  }
}
```
现在每个 counter 都有它自己内部的状态了：

* 扩展功能  比如：路由、ajax、数据流


 


