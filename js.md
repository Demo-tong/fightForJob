# JavaScript

- **介绍JavaScript的基本数据类型。**

> Undefined、Null、Boolean、Number、String

- **介绍js有哪些内置对象？**

> Object 是 JavaScript 中所有对象的父对象
> 
> 数据封装类对象：Object、Array、Boolean、Number 和 String

> 其他对象：Function、Arguments、Math、Date、RegExp、Error

- **说说写JavaScript的基本规范？**

> 1. 不要在同一行声明多个变量。

> 2. 请使用 ===/!== 来比较 true/false 或者数值

> 3. 使用对象字面量替代 new Array 这种形式

> 4. 不要使用全局函数。

> 5. Switch 语句必须带有 default 分支

> 6. 函数不应该有时候有返回值，有时候没有返回值

> 7. For 循环必须使用大括号

> 8. If 语句必须使用大括号

> 9. for~in 循环中的变量应该使用`var`关键字明确限定作用域，从而避免作用域污染

- **JavaScript原型，原型链 ? 有什么特点？**

> 每个对象都会在其内部初始化一个属性，就是 prototype(原型)，当我们访问一个对象的属性时，如果该对象内部不存在这个属性，那么它就会去 prototype 里找这个属性，这个 prototype 又会有自己的 prototype，于是就这样一直找下去，也就是我们平常所说的原型链的概念。

> 关系：instance.constructor.prototype === instace.__proto\__

> 特点：JavaScript 对象是通过引用来传递的，我们创建的每个新对象实体中并没有一份属于自己的原型副本。当我们修改原型时，与之相关的对象也会继承这一改变。

> 当我们需要一个属性时，JavaScript 引擎会先看当前对象中是否有这个属性，如果没有的话，就会查找它的 Prototype 对象是否有这个属性，如此递推下去，一直检索到 Object 内建对象。

	function Func(){}

    Func.prototype.name = "Sean";

    Func.prototype.getInfo = function() {
      return this.name;
    }

    var person = new Func(); //现在可以参考var person = Object.create(oldObject);
    console.log(person.getInfo()); //它拥有了Func的属性和方法 --- "Sean"
    console.log(Func.prototype); // Func { name="Sean", getInfo=function()}

- **JavaScript有几种类型的值？（堆：原始数据类型和 栈：引用数据类型），你能画一下他们的内存图吗？**

> 栈：原始数据类型（Undefined、Null、Boolean、Number、String）

> 堆：引用数据类型（对象、数组和函数）

> 两种类型的区别是：存储位置不同；

> 原始数据类型是直接存储在栈(Stack)中的简单数据段，占据空间小、大小固定，术语被频繁使用的数据；

> 引用数据类型是存储在堆(heap)中的对象，大小不固定，如果存储在栈中，将会影响程序运行的性能；引用数据类型在栈中存储了指针，该指针指向堆中该实体的起始位置。当解释器寻找引用值时，会首先检索其栈中的地址，取得地址后从堆中获得实体。

> [](stack-and-heap.jpg)

- **Javascript如何实现继承？**

> 1. 构造继承

> 2. 原型继承

> 3. 实例继承

> 4. 拷贝继承

> 原型 prototype 机制或 apply 和 call 方法去实现较简单，建议使用构造函数与原型混合方式。

 	function Parent(){
        this.name = 'wang';
    }

    function Child(){
        this.age = 28;
    }
    Child.prototype = new Parent(); //继承了Parent，通过原型

    var demo = new Child();
    alert(demo.age);
    alert(demo.name); //得到被继承的属性
  	}

- **JavaScript 继承的几种实现方式？**

> 参考：[构造函数的继承](http://www.ruanyifeng.com/blog/2010/05/object-oriented_javascript_inheritance.html)  [非构造函数的继承](http://www.ruanyifeng.com/blog/2010/05/object-oriented_javascript_inheritance_continued.html)

- **Javascript创建对象的几种方式？**

> 1. 对象字面量的方式

	person = {
		firstname: "Markk",
		lastname: "Yun",
		age : 25
	}

> 2. 用 function 来模拟无参的构造函数

	function Person() {
		var person = new Person();	//定义一个function，如果使用new“实例化”，该function可以看作是一个Class
		person.name = "Mark";
		person.age = 25;	
		person.work = function() {
			alert(person.name + "hello...");
		}	
	}

	person.work();

> 3. 用 function 来模拟带参的构造函数实现（用`this`关键字定义构造的上下文属性）

	function Pet(name,age,hobby) {
		this.name = name;
		this.age = age;
		this.hobby = hobby;
		this.eat = function() {
			alert("hello");
		}
	}
	
	var maidow = new Pet("Jack", 25, "codeing");
	maidow.eat();

> 4. 用工厂方式来创建（内置对象）

	var wcDog = new Object();
	wcDog.name = "旺财";
	wcDog.age = 3;
	wcDog.work = function() {
		alert("hello");
	}
	
	wcDog.work();

> 5. 用原型方式来创建

	function Dog() {}

	Dog.prototype.name = "旺财";
	Dog.prototype.eat = function() {
		alert(this.name + "是个吃货");
	}
	
	var wangcai = new Dog();
	wangcai.eat();

> 6. 用混合方式来创建

	function Car(name,price) {
		this.name = name;
		this.price = price;
	}
	
	Car.prototype.sell = function() {
		alert(this.name + this.price);
	}

	var camry = new Car("凯美瑞", 27);
	camry.sell();

- **Javascript作用链域?**

> 全局函数无法查看局部函数的内部细节，但局部函数可以查看其上层的函数细节，直至全局细节。

> 当需要从局部函数查找某一属性或方法时，如果当前作用域没有找到，就会上溯到上层作用域查找，直至全局函数，这种组织形式就是作用域链。

- **谈谈This对象的理解。**

> this 总是指向函数的直接调用者（而非间接调用者);

> 如果有 new 关键字，this 指向 new 出来的那个对象；

> 在事件中，this 指向触发这个事件的对象，特殊的是，IE 中的 attachEvent 中的 this 总是指向全局对象 window

- **eval是做什么的？**

> 它的功能是把对应的字符串解析成JS代码并运行；

> 应该避免使用`eval`，不安全，非常耗性能（2次，一次解析成JS语句，一次执行）；

> 由 JSNO 字符串转换为 JSON 对象时可以使用`eval`，`var obj = eavl('(' + str + ')');`


什么是window对象? 什么是document对象?

null，undefined的区别？

写一个通用的事件侦听器函数(机试题)。

["1", "2", "3"].map(parseInt) 答案是多少？

关于事件，IE与火狐的事件机制有什么区别？ 如何阻止冒泡？

- **什么是闭包（closure），为什么要用它？**

> 闭包是指有权访问另一个函数作用域中变量的函数，创建闭包的最常见的方式就是在一个函数内创建另一个函数，通过另一个函数访问这个函数的局部变量，利用闭包可以突破作用域链，将函数内部的变量和方法传递到外部。

> 闭包的特性：

> 1. 函数内再嵌套函数

> 2. 内部参数可以引用外层的参数和变量

> 3. 参数和变量不会被垃圾回收机制回收

javascript 代码中的"use strict";是什么意思 ? 使用它区别是什么？

如何判断一个对象是否属于某个类？

new操作符具体干了什么呢?

用原生JavaScript的实现过什么功能吗？

Javascript中，有一个函数，执行时对象查找时，永远不会去查找原型，这个函数是？

对JSON的了解？

[].forEach.call($$("*"),function(a){ a.style.outline="1px solid #"+(~~(Math.random()*(1<<24))).toString(16) }) 能解释一下这段代码的意思吗？

js延迟加载的方式有哪些？

Ajax 是什么? 如何创建一个Ajax？

同步和异步的区别?

如何解决跨域问题?

页面编码和被请求的资源编码如果不一致如何处理？

模块化开发怎么做？

AMD（Modules/Asynchronous-Definition）、CMD（Common Module Definition）规范区别？

requireJS的核心原理是什么？（如何动态加载的？如何避免多次加载的？如何 缓存的？）

让你自己设计实现一个requireJS，你会怎么做？

谈一谈你对ECMAScript6的了解？

ECMAScript6 怎么写class么，为什么会出现class这种东西?

异步加载的方式有哪些？

documen.write和 innerHTML的区别?

DOM操作——怎样添加、移除、移动、复制、创建和查找节点?

.call() 和 .apply() 的含义和区别？

数组和对象有哪些原生方法，列举一下？

JS 怎么实现一个类。怎么实例化这个类

JavaScript中的作用域与变量声明提升？

如何编写高性能的Javascript？

那些操作会造成内存泄漏？

JQuery的源码看过吗？能不能简单概况一下它的实现原理？

jQuery.fn的init方法返回的this指的是什么对象？为什么要返回this？

jquery中如何将数组转化为json字符串，然后再转化回来？

jQuery 的属性拷贝(extend)的实现原理是什么，如何实现深拷贝？

jquery.extend 与 jquery.fn.extend的区别？

jQuery 的队列是如何实现的？队列可以用在哪些地方？

谈一下Jquery中的bind(),live(),delegate(),on()的区别？

JQuery一个对象可以同时绑定多个事件，这是如何实现的？

是否知道自定义事件。jQuery里的fire函数是什么意思，什么时候用？

jQuery 是通过哪个方法和 Sizzle 选择器结合的？（jQuery.fn.find()进入Sizzle）

针对 jQuery性能的优化方法？

Jquery与jQuery UI有啥区别？

JQuery的源码看过吗？能不能简单说一下它的实现原理？

jquery 中如何将数组转化为json字符串，然后再转化回来？

jQuery和Zepto的区别？各自的使用场景？

针对 jQuery 的优化方法？

Zepto的点透问题如何解决？

jQueryUI如何自定义组件?

需求：实现一个页面操作不会整页刷新的网站，并且能在浏览器前进、后退时正确响应。给出你的技术实现方案？

如何判断当前脚本运行在浏览器还是node环境中？（阿里）

移动端最小触控区域是多大？

jQuery 的 slideUp动画 ，如果目标元素是被外部事件驱动, 当鼠标快速地连续触发外部元素事件, 动画会滞后的反复执行，该如何处理呢?

把 Script 标签 放在页面的最底部的body封闭之前 和封闭之后有什么区别？浏览器会如何解析它们？

移动端的点击事件的有延迟，时间是多久，为什么会有？ 怎么解决这个延时？（click 有 300ms 延迟,为了实现safari的双击事件的设计，浏览器要知道你是不是要双击操作。）

知道各种JS框架(Angular, Backbone, Ember, React, Meteor, Knockout...)么? 能讲出他们各自的优点和缺点么?

Underscore 对哪些 JS 原生对象进行了扩展以及提供了哪些好用的函数方法？

解释JavaScript中的作用域与变量声明提升？

那些操作会造成内存泄漏？

JQuery一个对象可以同时绑定多个事件，这是如何实现的？

Node.js的适用场景？

(如果会用node)知道route, middleware, cluster, nodemon, pm2, server-side rendering么?

解释一下 Backbone 的 MVC 实现方式？

什么是“前端路由”?什么时候适合使用“前端路由”? “前端路由”有哪些优点和缺点?

知道什么是webkit么? 知道怎么用浏览器的各种工具来调试和debug代码么?

如何测试前端代码么? 知道BDD, TDD, Unit Test么? 知道怎么测试你的前端工程么(mocha, sinon, jasmin, qUnit..)?

前端templating(Mustache, underscore, handlebars)是干嘛的, 怎么用?

简述一下 Handlebars 的基本用法？

简述一下 Handlerbars 的对模板的基本处理流程， 如何编译的？如何缓存的？

用js实现千位分隔符?(来源：前端农民工，提示：正则+replace)

检测浏览器版本版本有哪些方式？

我们给一个dom同时绑定两个点击事件，一个用捕获，一个用冒泡，你来说下会执行几次事件，然后会先执行冒泡还是捕获