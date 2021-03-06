## [小程序框架wepy文档链接](https://wepyjs.github.io/wepy/#/?id=%e5%b0%8f%e7%a8%8b%e5%ba%8f%e6%a1%86%e6%9e%b6wepy%e6%96%87%e6%a1%a3)
### 项目创建与使用
以下安装都通过npm安装

* 安装（更新） wepy 命令行工具。

```
npm install wepy-cli -g
```
* 在开发目录生成开发DEMO。

```
wepy new myproject
```
* 切换至项目目录。

```
cd myproject
```
* 开发实时编译。

```
wepy build --watch
```

### 项目目录结构
![](http://upload-images.jianshu.io/upload_images/3229842-15a7a8b1214cca84.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

### 开发使用说明
1. 使用微信开发者工具新建项目，本地开发选择``dist``目录。
2. 微信开发者工具-->项目-->关闭ES6转ES5。**重要：漏掉此项会运行报错。**
3. 微信开发者工具-->项目-->关闭上传代码时样式自动补全 **重要：某些情况下漏掉此项会也会运行报错。**
4. 微信开发者工具-->项目-->关闭代码压缩上传 **重要：开启后，会导致真机computed, props.sync 等等属性失效。**
5. 本地项目根目录运行wepy build --watch，开启实时编译。

### 主要解决问题
1. 开发模式转换
2. 支持组件化开发
3. 支持加载外部NPM包
4. 单文件模式，使得目录结构更加清晰
5. 默认使用babel编译，支持ES6/7的一些新特性。
6. 针对原生API进行优化

##### 下面对这几点分别进行说明
#### 1. 开发模式转换

>在原有的小程序的开发模式下进行再次封装，更贴近于现有MVVM框架开发模式。框架在开发过程中参考了一些现在框架的一些特性，并且融入其中

官方DEMO代码：

```
//index.js
//获取应用实例
var app = getApp()
Page({
    data: {
        motto: 'Hello World',
        userInfo: {}
    },
    //事件处理函数
    bindViewTap: function() {
        console.log('button clicked')
    },
    onLoad: function () {
        console.log('onLoad')
    }
})
```

基于wepy的实现：

```
import wepy from 'wepy';

export default class Index extends wepy.page {
    data = {
        motto: 'Hello World',
        userInfo: {}
    };
    methods = {
        bindViewTap () {
            console.log('button clicked');
        }
    };
    onLoad() {
        console.log('onLoad');
    };
}
```
#### 2. 支持组件化开发

```
// index.wpy
<template>
    <view>
        <panel>
            <h1 slot="title"></h1>
        </panel>
        <counter1 :num="myNum"></counter1>
        <counter2 :num.sync="syncNum"></counter2>
        <list :item="items"></list>
    </view>
</template>
<script>
import wepy from 'wepy';
import List from '../components/list';
import Panel from '../components/panel';
import Counter from '../components/counter';

export default class Index extends wepy.page {
    config = {
        "navigationBarTitleText": "test"
    };
    components = {
        panel: Panel,
        counter1: Counter,
        counter2: Counter,
        list: List
    };
    data = {
        myNum: 50,
        syncNum: 100,
        items: [1, 2, 3, 4]
    }
}
</script>
```

#### 3. 支持加载外部npm包

在编译过程当中，会递归遍历代码中的require然后将对应依赖文件从node_modules当中拷贝出来，并且修改require为相对路径，从而实现对外部NPM包的支持。如下图：
<br>
![](http://upload-images.jianshu.io/upload_images/3229842-a8e925f5a76a28d5.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
#### 4. 单文件模式，使得目录结构更加清晰

官方目录结构要求app必须有三个文件app.json，app.js，app.wxss，页面有4个文件 index.json，index.js，index.wxml，index.wxss。而且文件必须同名。
 
官方DEMO：
![](http://upload-images.jianshu.io/upload_images/3229842-3cfc25c127fed71a.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

使用wepy框架

```
project
└── src
    ├── coms
    |   └── child.wpy
    ├── pages
    |   ├── index.wpy    index 页面配置、结构、样式、逻辑
    |   └── log.wpy      log 页面配置、结构、样式、逻辑
    └──app.wpy           小程序配置项（全局样式配置、声明钩子等）
```

#### 5. 默认使用babel编译，支持ES6/7的一些新特性。
用户可以通过修改wepy.config.js(老版本使用.wepyrc)配置文件，配置自己熟悉的babel环境进行开发。默认开启使用了一些新的特性如promise，async/await等等。

```
import wepy from 'wepy';

export default class Index extends wepy.page {
    getData() {
        return new Promise((resolve, reject) => {
            setTimeout(() => {
                resolve({data: 123});
            }, 3000);
        });
    };
    async onLoad() {
        let data = await this.getData();
        console.log(data.data);
    };
}
```
#### 6. 针对原生API进行优化。
对现在API进行promise处理，同时修复一些现有API的缺陷，比如：wx.request并发问题等。 原有代码：

```
onLoad = function () {
    var self = this;
    wx.login({
        success: function (data) {
            wx.getUserInfo({
                success: function (userinfo) {
                    self.setData({userInfo: userinfo});
                }
            });
        }
    });
}
```
基于wepy实现代码：

```
import wepy from 'wepy';

async onLoad() {
    await wepy.login();
    this.userInfo = await wepy.getUserInfo();
}
```

在同时并发10个request请求测试时：不使用wepy,请求会发生错误。解决办法，使用wepy。


## wpy文件说明

``wpy``文件的编译过程:

![](http://upload-images.jianshu.io/upload_images/3229842-0018e73b15c5d811.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

一个.wpy文件分为三部分
1. 样式``<style></style>``对应原有``wxss``文件
2. 模板``<template></template>``对应原有``wxml``文件
3. 代码``<script></script>``对应原有``js``文件，分为两部分：1)逻辑部分，除了config对象之外的部分，对应于原生的.js文件;2）配置部分，即config对象，对应于原生的.json文件。




其中入口文件``app.wpy``不需要``template``,所以编译时会被忽略。这三个标签都支持``lang``和``src``属性，``lang``决定其代码编译过程，``src``决定是否外联代码，存在``src``属性且有效时，忽略内敛代码，示例如下：

```
<style lang="less" src="page1.less"></style>
<template lang="wxml" src="page1.wxml"></template>
<script>
    // some code
</script>
```
标签对应``lang``值如下表所示：


|  标签 |lang默认值  | lang支持值 |
| --- | --- | --- |
| style |css  |css,less,sass,style |
| template | wxml | wxml,xml,pug(原jade) |
| script | bable | bable,TypeScript |


## script 说明

#### 1. 程序入口 app.wpy

```
<style lang="less">
/** less **/
</style>
<script>
import wepy from 'wepy';
export default class extends wepy.app {
    config = {
        "pages":[
            "pages/index/index"
        ],
        "window":{
            "backgroundTextStyle": "light",
            "navigationBarBackgroundColor": "#fff",
            "navigationBarTitleText": "WeChat",
            "navigationBarTextStyle": "black"
        }
    };
    onLaunch() {
        console.log(this);
    }
}
</script>
```
页面入口``app.wpy``继承自``wepy.app``，包含一个``config``属性和其全局属性、方法、事件。其中``config``属性对应原有的``app.json``，编译时会根据``config``生成``app.json``文件，如果需要修改``config``中的内容，请使用系统提供API。


#### 2. 页面 index.wpy

```
<style lang="less">
/** less **/
</style>
<template lang="wxml">
    <view>
    </view>
    <counter1></counter1>
</template>
<script>
import wepy from 'wepy';
import Counter from '../components/counter';
export default class Index extends wepy.page {

    config = {};
    components = {counter1: Counter};

    data = {};
    methods = {};

    events = {};
    onLoad() {};
    // Other properties
}
</script>
```

页面入口继承自 ``wepy.page``，主要属性说明如下：

|属性	|说明|
|---|---|
|config	|页面配置对象，对应于原生的page.json文件，类似于app.wpy中的`config`|
|components	|页面组件列表对象，声明页面所引入的组件列表|
|data|	页面渲染数据对象，存放可用于页面模板绑定的渲染数据|
|methods|	wmxl的事件捕捉，如`bindtap`，`bindchange`|
|events	|	WePY组件事件处理函数对象，存放响应组件之间通过`$broadcast`、`$emit`、`$invoke`所传递的事件的函数|
|其它	|如`onLoad`，`onReady`等小程序事件以及其它自定义方法与属性|

#### 3.组件 com.wpy

```
<style lang="less">
/** less **/
</style>
<template lang="wxml">
    <view>  </view>
</template>
<script>
import wepy from 'wepy';
export default class Com extends wepy.component {

    components = {};

    data = {};
    methods = {};

    events = {};
    // Other properties
}
</script>
```
页面入口继承自``wepy.component``，属性与页面属性大致相同，除了不需要``config``以及页面特有的一些小程序事件等等。

## 实例

小程序在 WePY 中，被分为三个实例，App，Page，Component。其中Page实例继承自Component。声明方式如下：

```
import wepy from 'wepy';

// 声明一个App文件
export default class MyAPP extends wepy.app {
}
// 声明一个Page文件
export default class IndexPage extends wepy.page {
}
// 声明一个组件文件
export default class MyComponent extends wepy.component {
}
```
### App 实例

App小程序实例中主要包含小程序生命周期函数、config配置对象、globalData全局数据对象，以及其他自定义方法与属性。

```
import wepy from 'wepy';

export default class MyAPP extends wepy.app {
    customData = {};

    customFunction ()　{ }

    onLaunch () {}

    onShow () {}

    config = {}; // 对应 app.json 文件
    
    globalData = {}
}
```
在 Page 实例中，可以通过`this.$parent`来访问 App 实例。

### Page 和 Component 实例

由于`Page`页面实际上继承自`Component`组件，即`Page`也是组件。除扩展了页面所特有的`config`配置以及特有的页面生命周期函数之外，其它属性和方法与`Component`一致，因此这里以`Page`页面为例进行介绍。

```
import wepy from 'wepy';

// export default class MyPage extends wepy.page {
export default class MyComponent extends wepy.component {
    customData = {}  // 自定义数据

    customFunction ()　{}  //自定义方法

    onLoad () {}  // 在Page和Component共用的生命周期函数

    onShow () {}  // 只在Page中存在的页面生命周期函数

    config = {};  // 只在Page实例中存在的配置数据，对应于原生的page.json文件

    data = {};  // 页面所需数据均需在这里声明，可用于模板数据绑定

    components = {};  // 声明页面中所引用的组件，或声明组件中所引用的子组件

    mixins = [];  // 声明页面所引用的Mixin实例

    computed = {};  // 声明计算属性（详见后文介绍）

    watch = {};  // 声明数据watcher（详见后文介绍）

    methods = {};  // 声明页面wxml中标签的事件处理函数。注意，此处只用于声明页面wxml中标签的bind、catch事件，自定义方法需以自定义方法的方式声明

    events = {};  // 声明组件之间的事件处理函数
}
```
`methods `属性只声明页面`bind`，`catch`事件，不能声明自定义方法。

## 组件
小程序支持js模块化，但彼此独立，业务代码与交互事件仍需在页面处理。无法实现组件化的松耦合与复用的效果。 

wepy让小程序支持组件化开发，组件的所有业务与功能在组件本身实现，组件与组件之间彼此隔离，上述例子在wepy的组件化开发过程中，A组件只会影响到A绑定的myclick，B也如此。

### 普通组件引用

当页面或者组件需要引入子组件时，需要在页面或者 ``script``中的``components``给组件分配唯一ID，并且在``template``中添加``<component>``标签。

```
<template>
    <child></child>
</template>
<script>
    import wepy from 'wepy';
    import Child from './coms/child';
    export default class Index extends wepy.component {
        components = {
            child: Child
        };
    }
</script>
```
##### 注意：

WePY中的组件都是静态组件，是以组件ID作为唯一标识的，每一个ID都对应一个组件实例，当页面引入两个相同ID组件时，这两个组件共用同一个实例与数据，当其中一个组件数据变化时，另外一个也会一起变化。 如果需要避免这个问题，则需要分配多个组件ID和实例。

```
<template>
    <view class="child1">
        <child></child>
    </view>
    <view class="child2">
        <anotherchild></anotherchild>
    </view>

</template>
<script>
    import wepy from 'wepy';
    import Child from './coms/child';
    export default class Index extends wepy.component {
        components = {
            child: Child,
            anotherchild: Child
        };
    }
</script>
```

### ``<repeat>``的使用(循环列表组件引用)

当需要循环渲染`WePY`组件时(类似于通过`wx:for`循环渲染原生的`wxml`标签)，必须使用`WePY`定义的辅助标签`<repeat>`

```
<template>
    <repeat for="{{list}}" key="index" index="index" item="item">
        <child :item="item"></child>
    </repeat>
</template>
<script>
    import wepy from 'wepy';
    import Child from './coms/child';
    export default class Index extends wepy.component {
        components = {
            child: Child
        };
        data = {
            list: [{id: 1, title: 'title1'}, {id: 2, title: 'title2'}]
        }
    }
</script>
```
### ``computed`` 计算属性

* 类型: ``{ [key: string]: Function }``

* 详细： 

 1. computed计算属性，是一个有返回值的函数，可直接被当作绑定数据来使用。因此类似于data属性，代码中可通过this.计算属性名来引用，模板中也可通过{{ 计算属性名 }}来绑定数据。
 2. 只要是组件中有任何数据发生了改变，那么所有计算属性就都会被重新计算。

```
  data = {
      a: 1
  };

  computed = {
      aPlus () {
          return this.a + 1;
      }
  }
```
###``watcher`` 监听属性更新

* 类型: ``{ [key: string]: Function }``

* 详细： 

 1. 通过监听器watcher能够监听到任何属性的更新。监听器在watch对象中声明，类型为函数，函数名与需要被监听的data对象中的属性同名，每当被监听的属性改变一次，监听器函数就会被自动调用执行一次。

 2. 监听器适用于当属性改变时需要进行某些额外处理的情形。

```
  data = {
      num: 1
  };
  // 监听器函数名必须跟需要被监听的data对象中的属性num同名，
  // 其参数中的newValue为属性改变后的新值，oldValue为改变前的旧值
  watch = {
      num (newValue, oldValue) {
          console.log(`num value: ${oldValue} -> ${newValue}`)
      }
  }
  
  // 每当被监听的属性num改变一次，对应的同名监听器函数num()就被自动调用执行一次

  onLoad () {
      setInterval(() => {
          this.num++;
          this.$apply();
      }, 1000)
  }
```

### ``Props`` 传值

* 静态传值
* 动态传值

#### 静态传值
使用静态传值时，子组件会接收到字符串的值。

```
<child title="mytitle"></child>

// child.wpy
props = {
    title: String
};

onLoad () {
    console.log(this.title); // mytitle
}
```
注意：静态传值只能传递String类型，不存在Number，Boolean等类型。

#### 动态传值

动态传值是指父组件向子组件传递动态数据内容，父子组件数据完全独立互不干扰。但可以通过使用.sync修饰符来达到父组件数据绑定至子组件的效果，也可以通过设置子组件props的twoWay: true来达到子组件数据绑定至父组件的效果。那如果即使用.sync修饰符，同时子组件props中添加的twoWay: true时，就可以实现数据的双向绑定了。

注意：下文示例中的twoWay为true时，表示子组件向父组件单向动态传值，而twoWay为false(默认值，可不写)时，则表示子组件不向父组件传值。这是与Vue不一致的地方，而这里之所以仍然使用twoWay，只是为了尽可能保持与Vue在标识符命名上的一致性。

在父组件template模板部分所插入的子组件标签中，使用:prop属性（等价于Vue中的v-bind:prop属性）来进行动态传值。



```
// parent.wpy
<child :title="parentTitle" :syncTitle.sync="parentTitle" :twoWayTitle="parentTitle"></child>

data = {
    parentTitle: 'p-title'
};


// child.wpy
props = {
    title: String,
    syncTitle: {
        type: String,
        default: 'null'
    },
    twoWayTitle: {
        type: Number,
        default: 50,
        twoWay: true
    }
};

onLoad () {
    console.log(this.title); // p-title
    console.log(this.syncTitle); // p-title
    console.log(this.twoWayTitle); // 50

    this.title = 'c-title';
    console.log(this.$parent.parentTitle); // p-title.
    this.twoWayTitle = 60;
    console.log(this.$parent.parentTitle); // 60.  --- twoWay为true时，子组件props修改会改变父组件对应的值
    this.$parent.parentTitle = 'p-title-changed';
    console.log(this.title); // 'p-title';
    console.log(this.syncTitle); // 'p-title-changed' --- 有sync属性的props，当父组件改变时，会影响子组件的值。
}
```

## 组件通信与交互

``wepy.component``基类提供三个方法``$broadcast``，``$emit``，``$invoke``，因此任一页面或任一组件都可以调用这三种方法实现通信与交互。

组件的事件监听需要写在``events``属性下，如：

```
import wepy from 'wepy';
export default class Com extends wepy.component {

    components = {};

    data = {};
    methods = {};

    events = {
        'some-event': (p1, p2, p3, $event) => {
               console.log(`${this.name} receive ${$event.name} from ${$event.source.name}`);
        }
    };
    // Other properties
}
```

### $broadcast

``$broadcast`` 事件是由父组件发起，所有子组件都会收到此广播事件，除非事件被手动取消。事件广播的顺序为广度优先搜索顺序，如上图，如果``Page_Index``发起一个``$broadcast``事件，那么接收到事件的先后顺序为：A, B, C, D, E, F, G, H。如下图：
<br>
![](http://upload-images.jianshu.io/upload_images/3229842-67f0fb851e36b501.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

### $emit

``$emit``与``$broadcast``正好相反，事件发起组件的父组件会依次接收到``$emit``事件，如上图，如果E发起一个``$emit``事件，那么接收到事件的先后顺序为：``A, Page_Index``。

### $invoke

``$invoke``是一个组件对另一个组件的直接调用，通过传入的组件路径找到相应组件，然后再调用其方法。 如果想在``Page_Index``中调用组件A的某个方法

```
this.$invoke('ComA', 'someMethod', 'someArgs');
```
如果想在组件A中调用组件G的某个方法：

```
this.$invoke('./../ComB/ComG', 'someMethod', 'someArgs');
```
## 组件自定义事件

可以使用``@customEvent.user``绑定用户自定义组件事件。

其中，``@``表示事件修饰符，``customEvent ``表示事件名称，``.user``表示事件后缀。

目前有三种后缀：

``.default``: 绑定小程序冒泡事件事件，如``bindtap``。

``.stop``: 绑定小程序非冒泡事件，如``catchtap``。

``.user``: 绑定用户自定义组件事件，通过``$emit`触发。


```
// index.wpy
<template>
    <child @childFn.user="parentFn"></child>
</template>
<script>
    import wepy from 'wepy';
    import Child from './coms/child';
    export default class Index extends wepy.page {
        components = {
            child: Child
        };

        methods = {
            parentFn (num, evt) {
                console.log('parent received emit event, number is: ' + num)
            }
        }
    }
</script>


// child.wpy
<template>
    <view @tap="tap">Click me</view>
</template>
<script>
    import wepy from 'wepy';
    export default class Child extends wepy.component {
        methods = {
            tap () {
                console.log('child is clicked');
                this.$emit('childFn', 100);
            }
        }
    }
</script>
```

## 组件内容分发slot
WePY中的slot插槽作为内容分发标签的空间占位标签，便于在父组件中通过对相当于扩展板卡的内容分发标签的“插拔”，更为灵活、方便地对子组件进行内容分发。

具体使用方法是，首先在子组件template模板部分中声明slot标签作为内容插槽，同时必须在其name属性中指定插槽名称，还可设置默认的标签内容；然后在引入了该带有插槽的子组件的父组件template模板部分中声明用于“插拔”的内容分发标签。

注意，这些父组件中的内容分发标签必须具有slot属性，并且其值为子组件中对应的插槽名称，这样父组件内容分发标签中的内容会覆盖掉子组件对应插槽中的默认内容。

另外，要特别注意的是，父组件中一旦声明了对应于子组件插槽的内容分发标签，即便没有内容，子组件插槽中的默认内容也不会显示出来，只有删除了父组件中对应的内容分发标签，才能显示出来。

在Panel组件中有以下模板：

```
<view class="panel">
    <slot name="title">默认标题</slot>
    <slot>
        默认内容
    </slot>
</view>
```
在父组件使用Pannel组件时，可以这样使用：

```
<panel>
    <view>
        <text>这是我放到的内容</text>
    </view>
    <view slot="title">Panel的Title</view>
</panel>
```

## wepy 数据绑定
---
* 小程序数据绑定

```
this.setData({title: 'this is title'});
```
* wepy 数据绑定

```
this.title = 'this is title';
```
``wepy``使用脏数据检查对``setData``进行封装，在函数运行周期结束时执行脏数据检查，一来可以不用关心页面多次``setData``是否会有性能上的问题，二来可以更加简洁去修改数据实现绑定，不用重复去写``setData``方法。

但需注意，在函数运行周期之外的函数里去修改数据需要手动调用`$apply`方法。如：

```
setTimeout(() => {
    this.title = 'this is title';
    this.$apply();
}, 3000);
```

##  wx.request 接收参数
```
// 官方
wx.request({ 
       url: 'xxx',
       success: function (data) { 
             console.log(data); 
       }
});
// wepy 使用方式
wepy.request('xxxx').then((d) => console.log(d));
```

##  wepy 优化事件参数传递


#### 官方使用方法
```
<view data-id="{{index}}" data-title="wepy" data-other="otherparams" bindtap="tapName"> Click me! </view>
Page({
  tapName: function(event) {
    console.log(event.currentTarget.dataset.id)// output: 1
    console.log(event.currentTarget.dataset.title)// output: wepy
    console.log(event.currentTarget.dataset.other)// output: otherparams
  }
});
```
#### wepy 建议传参方式
```
<view data-wepy-params="{{index}}-wepy-otherparams" bindtap="tapName"> Click me! </view>
methods: {
    tapName (id, title, other, event) {
        console.log(id, title, other)// output: 1, wepy, otherparams
    }
}
```
#### wepy 1.1.8以后的版本，只允许传string。

```
<view bindtap="tapName({{index}}, 'wepy', 'otherparams')"> Click me! </view>
methods: {
    tapName (id, title, other, event) {
        console.log(id, title, other)// output: 1, wepy, otherparams
    }
}
```

## 组件代替模板和模块

----
官方

```
<!-- item.wxml -->
<template name="item">
  <text>{{text}}</text>
</template>

<!-- index.wxml -->
<import src="item.wxml"/>
<template is="item" data="{{text: 'forbar'}}"/>

<!-- index.js -->
var item = require('item.js')
```
 wepy
 
```
<!-- /components/item.wpy -->
 <text>{{text}}</text>

<!-- index.wpy -->
<template>
    <component id="item"></component>
</template>
<script>
    import wepy from 'wepy';
    import Item from '../components/item';
    export default class Index extends wepy.page {
        components = { Item }
    }
</script>
```

## API 
[API文档](https://wepyjs.github.io/wepy/#/api?id=api)
* [wepy.app Class](https://wepyjs.github.io/wepy/#/api?id=wepyapp-class)
App 基类，小程序入口。
* [wepy.component Class](https://wepyjs.github.io/wepy/#/api?id=wepycomponent-class)
组件基类
* [wepy.page Class](https://wepyjs.github.io/wepy/#/api?id=wepypage-class)
页面类，继承自wepy.component，拥有页面所有的属性与方法。
* [wepy.event Class](https://wepyjs.github.io/wepy/#/api?id=wepyevent-class)
小程序事件封装类
* [wepy.mixin Class](https://wepyjs.github.io/wepy/#/api?id=wepymixin-class)
Mixin基类，用于复用不同组件中的相同功能。

