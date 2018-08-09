## null  undefined

null与undefined都可以表示“没有”，含义非常相似。

在if语句中，它们都会被自动转为false，相等运算符（==）甚至直接报告两者相等。

```
if (!undefined) {
  console.log('undefined is false');
}
// undefined is false

if (!null) {
  console.log('null is false');
}
// null is false

undefined == null
// true
```
##### 既然含义与用法都差不多，为什么要同时设置两个这样的值?

1995年 JavaScript 诞生时，最初像 Java 一样，只设置了null表示"无"。根据 C 语言的传统，null可以自动转为0。

```
Number(null) // 0
5 + null // 5

```

但是，JavaScript 的设计者 Brendan Eich，觉得这样做还不够。首先，第一版的 JavaScript 里面，null就像在 Java 里一样，被当成一个对象，Brendan Eich 觉得表示“无”的值最好不是对象。其次，那时的 JavaScript 不包括错误处理机制，Brendan Eich 觉得，如果null自动转为0，很不容易发现错误。

因此，他又设计了一个undefined。区别是这样的：null是一个表示“空”的对象，转为数值时为0；undefined是一个表示"此处无定义"的原始值，转为数值时为NaN。

```
Number(undefined) // NaN
5 + undefined // NaN
```

undefined表示“未定义”，下面是返回undefined的典型场景。

```
// 变量声明了，但没有赋值
var i;
i // undefined

// 调用函数时，应该提供的参数没有提供，该参数等于 undefined
function f(x) {
  return x;
}
f() // undefined

// 对象没有赋值的属性
var  o = new Object();
o.p // undefined

// 函数没有返回值时，默认返回 undefined
function f() {}
f() // undefined
```

### 布尔值

布尔值代表“真”和“假”两个状态。“真”用关键字true表示，“假”用关键字false表示。布尔值只有这两个值。


如果 JavaScript 预期某个位置应该是布尔值，会将该位置上现有的值自动转为布尔值。转换规则是除了下面六个值被转为false，其他值都视为true。

* undefined
* null
* false
* 0
* NaN
* ""或''（空字符串）

***注意，空数组（[]）和空对象（{}）对应的布尔值，都是true。***


