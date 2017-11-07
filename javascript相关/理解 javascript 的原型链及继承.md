# 理解 javascript 的原型链及继承

```javascript
class Shape{}
class Circle extends Shape{}
const circle = new Circle();

console.log(circle.__proto__ === Circle.prototype);
console.log(Circle.prototype.__proto__ === Shape.prototype);
console.log(Shape.prototype.__proto__ === Object.prototype);
console.log(Object.prototype.__proto__ === null);

console.log(Circle.__proto__ === Shape);
console.log(Shape.__proto__ === Function.prototype);
console.log(Function.prototype.__proto__ === Object.prototype);
console.log(Object.prototype.__proto__ === null);

console.log(circle.constructor === Circle)
```

以上所有的运行结果都是 ``true``;

![](http://upload-images.jianshu.io/upload_images/3229842-995c2149013a4d80.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)



### 三种构造对象的方法：

###### 1. 通过对象字面量构造。

```
var person1 = {
    name: 'cyl',
    sex: 'male'
};
```
形如这个形式的叫做对象字面量。这样子构造出的对象，其[[prototype]]指向Object.prototype
###### 2.  构造函数构造。

```
function Person(){}
var person1 = new Person();
```
通过new操作符调用的函数就是构造函数。由构造函数构造的对象，其[[prototype]]指向其构造函数的prototype属性指向的对象。每个函数都有一个prototype属性，其所指向的对象带有constructor属性，这一属性指向函数自身。（在本例中，person1的[[prototype]]指向Person.prototype）
###### 3. 函数Object.create构造的。

```
var person1 = {
    name: 'cyl',
    sex: 'male'
};

var person2 = Object.create(person1);
```

本例中，对象person2的[[prototype]]指向对象person1。在没有Object.create函数的日子里，人们是这样做的：

```
Object.create = function(p) {
    function f(){}
    f.prototype = p;
    return new f();
}
```
### 一、原型

##  ``__proto__``（隐式原型）

每个JS对象一定对应一个原型对象，并从原型对象继承属性和方法。

对象__proto__属性的值就是它所对应的原型对象，隐式原型指向创建这个对象的函数(constructor)的prototype。

JavaScript中任意对象都有一个内置属性[[prototype]]，在ES5之前没有标准的方法访问这个内置属性，但是大多数浏览器都支持通过__proto__来访问。ES5中有了对于这个内置属性标准的Get方法Object.getPrototypeOf().                     
Object.prototype 这个对象是个例外，它的__proto__值为null



```
var one = {x: 1};
var two = new Object();
console.log(one.__proto__ === Object.prototype)//true
console.log(two.__proto__ === Object.prototype)//true
```

#### 作用：
 隐式原型的作用：构成原型链，同样用于实现基于原型的继承。举个例子，当我们访问obj这个对象中的x属性时，如果在obj中找不到，那么就会沿着__proto__依次查找。

## prototype（显式原型）

不像每个对象都有__proto__属性来标识自己所继承的原型，只有函数才有prototype属性。

JS不像其它面向对象的语言，它没有类（class，ES6引进了这个关键字，但更多是语法糖）的概念。JS通过函数来模拟类。

当你创建函数时，JS会为这个函数自动添加prototype属性，值是空对象。而一旦你把这个函数当作构造函数（constructor）调用（即通过new关键字调用），那么JS就会帮你创建该构造函数的实例，实例继承构造函数prototype的所有属性和方法（实例通过设置自己的__proto__指向承构造函数的prototype来实现这种继承）。


JS是单继承的，Object.prototype是原型链的顶端，所有对象从它继承了包括toString等等方法和属性。Object.prototype.__proto__ === null，说明原型链到Object.prototype终止。

#### 作用：
 显式原型的作用：用来实现基于原型的继承与属性的共享。

****

Object本身是构造函数，继承了Function.prototype;Function也是对象，继承了Object.prototype。

```
Object instanceof Function // true
Function instanceof Object // true
```

instanceof 运算符用来测试一个对象在其原型链中是否存在一个构造函数的prototype 属性。

ES规范是怎么说的？

Function本身就是函数，Function.__proto__是标准的内置对象Function.prototype。
Function.prototype.__proto__是标准的内置对象Object.prototype。


### 例一

```
//函数声明创一个空函数
function foo(){}

```

![3229842-48de74a3cfec7e9d](http://upload-images.jianshu.io/upload_images/3229842-3d153bd991372d38.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)



foo这个函数就有个prototype属性，并且它默认有两个属性:constructor和__proto__。constructor属性会指向它本身foo，__proto__是在chrome中暴露的(不是一个标准属性)，那么foo.prototype的原型会指向Object.prototype。因此Object.prototype上的一些方法toString，valueOf才会被每个一般的对象所使用。

### 例二

```
function foo(){}
foo.prototype.x = 1;
var obj3 = new foo();//实例对象
console.log(obj3.x); //1
```


我们这里有个foo函数，这个函数有个prototype的对象属性，它的作用就是当使用new foo()去构造实例的时候，这个构造器的prototype属性会用作new出来的这些对象的原型。

>在这个例子中，obj3.__proto__===foo.prototype,即，每个对象都有一个__proto__属性，指向创建该对象的函数的prototype。Object.prototype是一个特例，它的__proto__指向的是null。

### 例三

```
// 声明构造函数
function Person(name, age) {
    this.name = name;
    this.age = age;
}

// 通过prototye属性，将方法放到原型对象上
Person.prototype.getName = function() {
    return this.name;
}

var p1 = new Person('tim', 10);
var p2 = new Person('jak', 22);
```

![3229842-3e7187f42cdfcda9](http://upload-images.jianshu.io/upload_images/3229842-3e7187f42cdfcda9.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

构造函数的prototype与所有实例对象的__proto__都指向原型对象。而原型对象的constructor指向构造函数。

### 二、原型链
>每一个构造函数都有一个原型对象，当我们让某一原型对象等于另一构造函数的实例，此时该原型对象就包含一个指针，该指针指向这一构造函数的原型对象，该指针指向的原型对象中包含一个指向这一构造函数的指针，同样我们可以令该指针指向的原型对象等于另一构造函数的实例，如此递进，则形成一条实例与原型的链条，即原型链。

````
 function Parent() {
        this.name = 'parent';
    };
    Parent.prototype.getName = function() {
        return this.name;
    };
    function Child() {
        this.childname = 'child';
    }
    Child.prototype = new Parent();
    Child.prototype.getChildName = function() {
        return this.childname;
    };
    var child = new Child();
    console.log(child.getName()); //输出parent
    console.log(child.getChildName());  //输出child
````
在上面的例子中，child实例指向Child原型，Child原型等于Parent实例，即指向Parent原型。可见本质即是以一个构造函数的实例重写原型对象，形成原型链。

>#### 总结
###### 1、所有的对象都有 __proto__ 属性，该属性对应该对象的原型；
###### 2、所有的函数对象都有 prototype 属性，该属性的值会被赋值给该函数创建的对象的 __proto__属性；
###### 3、所有的原型对象都有constructor属性，该属性对应创建所有指向该原型的实例的构造函数；
###### 4、函数对象和原型对象通过prototype和constructor属性进行相互关联。

## extends

用关键词extends声明子类关系：

```
    class Circle extends Shape {}
```
extends后面可以接驳任意合法且拥有prototype属性的构造函数。它可以是：

<br>另一个类
<br>源自现有继承框架（译者注：作者指的是原型继承，即使在JavaScript中类继承的本质也是原型继承）的近类函数
<br>一个普通的函数
<br>一个包含一个函数或类的变量
<br>一个对象上的属性访问
<br>一个函数调用


### 图示
![](http://upload-images.jianshu.io/upload_images/3229842-006f1ec28f6d3238.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
<br>1.  在JS里，万物皆对象。方法（Function）是对象，方法的原型(Function.prototype)是对象。因此，它们都会具有对象共有的特点。即：对象具有属性__proto__，可称为隐式原型，一个对象的隐式原型指向构造该对象的构造函数的原型，这也保证了实例能够访问在构造函数原型中定义的属性和方法。
<br>2.  方法(Function)方法这个特殊的对象，除了和其他对象一样有上述_proto_属性之外，还有自己特有的属性——原型属性（prototype），这个属性是一个指针，指向一个对象，这个对象的用途就是包含所有实例共享的属性和方法（我们把这个对象叫做原型对象）。原型对象也有一个属性，叫做constructor，这个属性包含了一个指针，指回原构造函数。

### 上图解析
<br>1.构造函数Foo()构造函数的原型属性Foo.prototype指向了原型对象，在原型对象里有共有的方法，所有构造函数声明的实例（这里是f1，f2）都可以共享这个方法。
<br>2.原型对象Foo.prototypeFoo.prototype保存着实例共享的方法，有一个指针constructor指回构造函数。
<br>3.实例f1和f2是Foo这个对象的两个实例，这两个对象也有属性__proto__，指向构造函数的原型对象，这样子就可以像上面1所说的访问原型对象的所有方法啦。另外：构造函数Foo()除了是方法，也是对象啊，它也有__proto__属性，指向谁呢？指向它的构造函数的原型对象呗。函数的构造函数不就是Function嘛，因此这里的__proto__指向了Function.prototype。其实除了Foo()，Function(), Object()也是一样的道理。原型对象也是对象啊，它的__proto__属性，又指向谁呢？同理，指向它的构造函数的原型对象呗。这里是Object.prototype.最后，Object.prototype的__proto__属性指向null。

#### 总结：
* 对象有属性__proto__,指向该对象的构造函数的原型对象。
* 方法除了有属性__proto__,还有属性prototype，prototype指向该方法的原型对象。
