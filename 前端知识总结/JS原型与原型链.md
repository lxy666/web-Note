### 一、原型
JavaScript中创建的每一个函数，都有一个prototype属性，该属性是一个指针，指向一个对象。这个对象，就是我们这里说的原型。
所有的原型对象都会有一个constructor属性，这个属性包含一个指向prototype属性所在函数的指针。
```javascript
//函数声明创一个空函数
function foo(){}
```

![原型.png](http://upload-images.jianshu.io/upload_images/3229842-48de74a3cfec7e9d.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

foo这个函数就有个prototype属性，并且它默认有两个属性:constructor和__proto__。constructor属性会指向它本身foo，__proto__是在chrome中暴露的(不是一个标准属性)，那么foo.prototype的原型会指向Object.prototype。因此Object.prototype上的一些方法toString，valueOf才会被每个一般的对象所使用。
```
function foo(){}
foo.prototype.x = 1;
var obj3 = new foo();//实例对象
```

![实例对象](http://upload-images.jianshu.io/upload_images/3229842-1ec041fa1df1e55f.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

我们这里有个foo函数，这个函数有个prototype的对象属性，它的作用就是当使用new foo()去构造实例的时候，这个构造器的prototype属性会用作new出来的这些对象的原型。
>在这个例子中，obj3.__proto__===foo.prototype,即，每个对象都有一个__proto__属性，指向创建该对象的函数的prototype。Object.prototype是一个特例，它的__proto__指向的是null。

#### 下面是一个例子
````
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
````

![图示.png](http://upload-images.jianshu.io/upload_images/3229842-3e7187f42cdfcda9.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

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
