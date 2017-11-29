## 组件wxml的slot

>在组件的wxml中可以包含 slot 节点，用于承载组件使用者提供的wxml结构。

默认情况下，一个组件的wxml中只能有一个slot。需要使用多slot时，可以在组件js中声明启用。

```

Component({
  options: {
    multipleSlots: true // 在组件定义时的选项中启用多slot支持
  },
  properties: { /* ... */ },
  methods: { /* ... */ }
})

```

此时，可以在这个组件的wxml中使用多个slot，以不同的 name 来区分。

```
<!-- 组件模板 -->
<view class="wrapper">
  <slot name="before"></slot>
  <view>这里是组件的内部细节</view>
  <slot name="after"></slot>
</view>
```


使用时，用 slot 属性来将节点插入到不同的slot上。

```
<!-- 引用组件的页面模版 -->
<view>
  <component-tag-name>
    <!-- 这部分内容将被放置在组件 <slot name="before"> 的位置上 -->
    <view slot="before">这里是插入到组件slot name="before"中的内容</view>
    <!-- 这部分内容将被放置在组件 <slot name="after"> 的位置上 -->
    <view slot="after">这里是插入到组件slot name="after"中的内容</view>
  </component-tag-name>
</view>
```

## wepy

>WePY中的slot插槽作为内容分发标签的空间占位标签，便于在父组件中通过对相当于扩展板卡的内容分发标签的“插拔”，更为灵活、方便地对子组件进行内容分发。

具体使用方法是，首先在子组件template模板部分中声明slot标签作为内容插槽，同时必须在其name属性中指定插槽名称，还可设置默认的标签内容；然后在引入了该带有插槽的子组件的父组件template模板部分中声明用于“插拔”的内容分发标签。

* 注意，这些父组件中的内容分发标签必须具有slot属性，并且其值为子组件中对应的插槽名称，这样父组件内容分发标签中的内容会覆盖掉子组件对应插槽中的默认内容。

* 另外，要特别注意的是，父组件中一旦声明了对应于子组件插槽的内容分发标签，即便没有内容，子组件插槽中的默认内容也不会显示出来，只有删除了父组件中对应的内容分发标签，才能显示出来。

示例：

在Panel组件中有以下模板：

![](https://ws3.sinaimg.cn/large/006tKfTcly1flz6yycaz0j30jc088mxz.jpg)

在父组件中使用Pannel子组件时，可以这样使用：

![](https://ws3.sinaimg.cn/large/006tKfTcly1flz70cimtij30kg09g0tl.jpg)

示例：带有 repeat 的slot

父组件：Page

```
<template>
  <view >
    <repeat for=“{{list}}" key="id" item="item">
      <slot></slot>
    </repeat>
  </view>
</template>
<script>
  import wepy         from 'wepy';
  import Item  from './Item’; // 子组件内使用的组件，子组件不用引用
  export default class ListPage extends wepy.component {
    components = {
      Item
    };
    data = {
     List: [],
    }
  }
</script>
```
子组件：

```
<template>
  <Page>
    <Item :list.sync="item" :openType="openType" />
  </Page>
</template>
```
Ps: 属性可以直接写在 slot 的行间的
