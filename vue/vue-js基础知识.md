>###vue
一个mvvm框架（库），类似于angular，拥有比较容易上手的AIP。它是一套构建用户界面的 渐进式框架。与其他重量级框架不同的是，Vue 采用自底向上增量开发的设计。Vue 的核心库只关注视图层，并且非常容易学习，非常容易与其它库或已有项目整合。另一方面，Vue 完全有能力驱动采用单文件组件和Vue生态系统支持的库开发的复杂单页应用。

####下面我们来了解一下MVC、MVP及MVVM模式框架
#####1.MVC
     Model(模型)+View(视图)+controller(控制器)，主要是基于分层的目     的，让彼此的职责分开。
     View通过Controller来和Model联系，Controller是View和Model的协调者，View和Model不直接联系，基本联系都是单向的。
     用户User通过控制器Controller来操作模板Model从而达到视图View的变化。
#####2.MVP：
    从MVC模式演变而来的，都是通过Controller/Presenter负责逻辑的处理+Model提供数据+View负责显示。
    在MVP中，Presenter完全把View和Model进行了分离，主要的程序逻辑在Presenter里实现。
    并且，Presenter和View是没有直接关联的，是通过定义好的接口进行交互，从而使得在变更View的时候可以保持Presenter不变。
    MVP模式的框架：Riot,js。
#####3.MVVM
    MVVM是把MVC里的Controller和MVP里的Presenter改成了    ViewModel。Model+View+ViewModel。
    View的变化会自动更新到ViewModel,ViewModel的变化也会自动同步到View上显示。
    这种自动同步是因为ViewModel中的属性实现了Observer，当属性变更时都能触发对应的操作。
    MVVM模式的框架有：AngularJS+Vue.js和Knockout+Ember.js后两种知名度较低以及是早起的框架模式。

>其实Vue.js自身不是一个全能的框架，因为它只聚焦视图层，是一个构建数据驱动的Web界面的库。
Vue.js通过简单的API（应用程序编程接口）提供高效的数据绑定和灵活的组件系统。

#####Vue.js的特性如下：
* 轻量级的框架
* 双向数据绑定
* 指令
* 插件化

 ###Vue.js与其他框架的区别？
####1.与angularjs的区别
#####相同点：
都支持指令：内置指令和自定义指令。
都支持过滤器：内置过滤器和自定义过滤器。
都支持双向数据绑定。
都不支持低端浏览器。
#####不同点：
1.AngularJS的学习成本高，比如增加了Dependency Injection特性，而Vue.js本身提供的API都比较简单、直观。
2.在性能上，AngularJS依赖对数据做脏检查，所以Watcher越多越慢。
Vue.js使用基于依赖追踪的观察并且使用异步队列更新。所有的数据都是独立触发的。
对于庞大的应用来说，这个优化差异还是比较明显的。
####2.与React的区别
#####相同点：
react采用特殊的JSX语法，Vue.js在组件开发中也推崇编写.vue特殊文件格式，对文件内容都有一些约定，两者都需要编译后使用。
中心思想相同：一切都是组件，组件实例之间可以嵌套。
都提供合理的钩子函数，可以让开发者定制化地去处理需求。
都不内置列数AJAX，Route等功能到核心包，而是以插件的方式加载。
在组件开发中都支持mixins的特性。
#####不同点：
React依赖Virtual DOM,而Vue.js使用的是DOM模板。React采用的Virtual DOM会对渲染出来的结果做脏检查。
Vue.js在模板中提供了指令，过滤器等，可以非常方便，快捷地操作DOM。

***

#####Hello world样例
````
<div id="app">
    {{ message }}
</div>
var app = new Vue({
    el: '#app',
    data: {
       message: 'Hello world!'
    }
})
````
>####浏览器渲染结果：
    Hello world!
Vue使数据和 DOM 被绑定在一起，所有的元素都是响应式的。当app.message改变时，会引起DOM的重新渲染。

####Vue实例
````
 //选项对象
<div id='app'>

</div>
var vm = new Vue({
// 选项对象
})
````
在实例化 Vue 时，需要传入一个选项对象。
选项对象包含常用的属性包括，在下文还会进行拓展：
````
var vm = { 
   el:'', // 以CSS选择器的形式选择根元素
   data:{
     message:'Hello world!' 
   }, // 数据对象
   methods:{ 
        sayHello:function () {
           alert(this.message) } 
        }, //方法对象
}
````
>###vue指令
#####vue拥有一套指令系统。所谓指令 ，就是在模板中出现的带有 v-前缀，当其表达式的值改变时相应地将这些行为应用到 DOM元素上。指令能够实现条件渲染，列表渲染，绑定属性等功能。
####下面讲了七个指令：
######1、v-if 条件渲染指令，根据其后表达式的bool值进行判断是否渲染该元素；
######2、v-show 与v-if类似，只是会渲染其身后表达式为false的元素，而且会给这样的元素添加css代码：style="display:none";
######3、 v-else 必须跟在v-if/v-show指令之后，不然不起作用；如果v-if/v-show指令的表达式为true，则else元素不显示；如果v-if/v-show指令的表达式为false，则else元素会显示在页面上；
######4、 v-for  类似JS的遍历，用法为 v-for="item in items", items是数组，item为数组中的数组元素。
######5、 v-bind  这个指令用于响应地更新 HTML 特性，比如绑定某个class元素或元素的style样式。
######6、 v-on  用于监听指定元素的DOM事件，比如点击事件。
######7、v-model 用于表单元素，进行双向数据绑定。
