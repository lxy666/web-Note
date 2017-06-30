## 匿名函数
* JavaScript函数可以是匿名的。这意味着你可以从函数声明中省略函数名。但是，函数必须存储在变量中。
* ``var addNumbers = function (x, y) { return x + y; }``上述语法被也被称为函数表达式。
* 你可以把变量addNumbers 当作函数名，以及像下面这样调用该函数。``var sum = addNumbers(2, 3);``

* 当你想传递一个函数作为参数给另一个函数时，函数表达式就非常方便了。让我们用一个简单的例子来试着了解这一点。
```
var add = function (first, second) { return first + second };
var multiply = function (first, second) { return first * second };
function calculate(fun, a, b) {   
return fun(a, b);
}
```
>首先我已经创建了两个匿名函数。第一个返回两个数的加法运算，第二个返回两个数的乘法运算。相当简单，没有什么可值得炫耀的地方。然后，我定义函数calculate，这个函数接受函数作为第一个参数后跟两个参数接受两个数字。我可以通过传递任意函数作为第一个参数来调用函数calculate。

```
var sum = calculate(add, 2, 3); // sum = 5
var multiplication = calculate(multiply, 2, 3); // multiplication = 6
```

## 关于参数
### 缺少参数
调用函数时，函数的参数数量可以比要求的更少或更多。如果你调用的函数的参数比声明的少，那么缺少的参数被设置为undefined。
```
function callMe(a, b, c) {
   console.log("c is " + typeof c);
}
callMe("Code", "Morning"); // c is undefined
callMe("Learn", "JavaScript", "Functions"); //  c is string
```

### Arguments对象
所有的JavaScript函数有一个特殊的对象，叫做arguments，它是在函数调用过程中传递的参数数组。该对象可以被用来访问单个参数或获得传递到函数的参数总数。
```
function callMe() {
   var i;  
   for (i = 0; i < arguments.length; i++) {     
   console.log(arguments[i]);
   }
   console.log("Total arguments passed: " + arguments.length);
}
```
>此函数假设没有传递任何参数，但就像我说的，你可以传递任何数量的参数到JavaScript函数。我可以像这样调用这个函数：``callMe("Code", "Morning", "Mr. Programmer");//  Code Morning Mr.Programmer Total arguments passed: 3``每个参数可以从arguments对象作为一个数组项被访问。被传递给函数的arguments的总数可从arguments.length属性获得。

### 默认参数
```
function greetMyVisitors(name, profession = "The cool programmer") {
    alert("Welcome Mr. " + name + ", " + profession);
}
//该函数有礼貌地地迎接了博客访问者。它有两个参数name 和profession，并在消息框中显示一个欢迎消息。
//如果在调用过程中没有参数（或“undefined”）传递，那么第二个参数取用默认值。

greetMyVisitors("Justin Bieber", "The singer"); 
//Welcome Mr. Justin Bieber, The singer

greetMyVisitors("Bob Martin"); 
// Welcome Mr. Bob Martin, The cool programmer

greetMyVisitors("John Papa", undefined); 
// Welcome Mr. John Papa, The cool programmer
```
## 嵌套函数

函数可以在它的内部包含一个或多个函数。内部函数可能会在内部再次包含函数。
```
function wakeUpAndCode() {   

function wakeUp() {     
console.log("I just woke up");
   }   

function code() {    
 console.log("I am ready to code now");
   }

   wakeUp();
   code();
}
wakeUpAndCode();//  I just woke up   I am ready to code now
```
函数``wakeUpAndCode``包含两个内部函数``wakeUp``和``code``。当调用``wakeUpAndCode``时，函数主体开始执行函数主体。在外部函数中只有两个可执行语句，调用``wakeUp``和``code``的方法。调用``wakeUp``将执行内部``wakeUp``函数，这将写入``I just woke up``到控制台。调用``code``将会写入``I am ready to code now``到控制台。内部函数可以访问所有外部函数的变量和参数。内部函数是函数内部某种private实现，并且不能从外部函数以外被调用。
## 立即执行函数表达式
```
(function() { 
  // Your code here
}());
```
* 所有你要做的就是创建一个匿名函数，在函数定义后马上放一对圆括号以调用函数，最后将所有代码封装在另一对圆括号中。最外层的括号将它里面的所有一切转变成一个表达式，因为括号不能包含JavaScript语句。函数定义后面的圆括号则立即调用函数。

* 这其中定义的任何变量或函数不能被这个范围以外的任何代码改变。

* 这是一个在代码中创建局部范围的很好方法。它们可以帮助你保护变量和函数，以避免被应用程序的其他部分更改或覆盖。
##构造函数

>函数可以充当构造器的角色，并且可以使用构造函数来创建新的对象。这是JavaScript面向对象的特点之一。使用构造函数的好处是，你将能够通过预定义的属性和方法，创造尽可能多的对象。

```
function Programmer(name, company, expertise) {  
this.name = name;   
this.company = company;  
this.expertise = expertise;  
this.writeCode = function() {     
console.log("Writing some public static thing..");
   }   
this.makeSkypeCall = function() {    
  console.log("Making skype call..");
   }  
this.doSalsa = function() {    
  console.log("I'm a programmer, I can only do Gangnam style..");
   }  
this.canWriteJavaScript = function() {     
  return expertise === "JavaScript";
   }
}
```
>函数有三个参数，并创建了一个具有三个属性和四种方法的对象。
``var javaProgrammer = new Programmer("Mohit Srivastava", "Infosys", "Java”);
var dotnetProgrammer = new Programmer("Atul Mishra", "Prowareness", ".NET");``
虽然也可以创建一个使用对象文本语法带有相同属性和方法的对象，但我们需要多次编写相同的代码。构造函数使得可以一次定义对象，并创建真正的实例。

## 注意
###### 始终使用new关键字来从构造器创建新的对象。

* ``var jsProgrammer = Programmer("Douglas Crockford", "Yahoo", "JavaScript")``        
最终将添加所有属性和方法到全局的window对象，原因是，除非明确指定，否则“this”指向全局的window对象。使用new 设置“this”上下文到被创建的当前对象。

* 然而，有一种变通方法可以来克服这个问题。你可以改变构造函数的实现以使域安全，然后在创建新的对象时，你就可以愉快地忽略new 关键字了。请参见以下修改了的构造函数代码。
```
function Programmer(name, company, expertise) {  
if(!(this instanceof Programmer)) {     
    return new Programmer(name, company, expertise);
   }  
this.name = name; 
this.company = company;   
this.expertise = expertise;   
this.writeCode = function() {     
console.log("Writing some public static thing..");
   }
}
```
``
if 条件检查了this 对象是否是Programmer的一个实例。如果不是，它会创建一个新的Programmer对象，并通过再次调用构造器返回相同的内容。
``
>注意：你无法在不使用’new’关键字的情况下，在Strict模式下从构造器创建一个新的对象。Strict模式强制一些编码准则，并且在你写的东西不安全的情况下会抛出错误。要启用Strict模式，你只需要添加在你的代码开头添加字符串 ‘use strict’。在Strict模式下运行代码是一个良好的实践。
```
'use strict'
 function doSomething() { ... }
```
