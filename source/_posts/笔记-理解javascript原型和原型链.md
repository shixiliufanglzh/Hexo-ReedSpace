---
title: '[笔记]理解javascript原型和原型链'
tags: javascript
categories: 前端开发
abbrlink: 14180
date: 2020-10-24 22:21:16
---

&emsp;&emsp;`new`运算符从构造器中得到一个对象，下面的代码我们再熟悉不过了：
```javascript
function Person( name ){
    this.name = name;
};

Person.prototype.getName = function(){
    return this.name;
};

var a = new Person( 'sven' )

console.log( a.name );    // 输出：sven
console.log( a.getName() );     // 输出：sven
console.log( Object.getPrototypeOf( a ) === Person.prototype );     // 输出：true
```

&emsp;&emsp;在这里`Person`并不是类，而是函数构造器，JavaScript的函数既可以作为普通函数被调用，也可以作为构造器被调用。当使用`new`运算符来调用函数时，此时的函数就是一个构造器。 用`new`运算符来创建对象的过程，实际上也只是先克隆`Object.prototype`对象，再进行一些其他额外操作的过程。

&emsp;&emsp;在Chrome和Firefox等向外暴露了对象`__proto__`属性的浏览器下，我们可以通过下面这段代码来理解`new`运算的过程：
```javascript
function Person( name ){
    this.name = name;
};

Person.prototype.getName = function(){
    return this.name;
};

var objectFactory = function(){
    var obj = new Object(),    // 从Object.prototype上克隆一个空的对象
        Constructor = [].shift.call( arguments );    // 取得外部传入的构造器，此例是Person

    obj.__proto__ = Constructor.prototype;    // 指向正确的原型
    var ret = Constructor.apply( obj, arguments );    // 借用外部传入的构造器给obj设置属性
    return typeof ret === 'object' ? ret : obj;     // 确保构造器总是会返回一个对象
};

var a = objectFactory( Person, 'sven' );

console.log( a.name );    // 输出：sven
console.log( a.getName() );     // 输出：sven
console.log( Object.getPrototypeOf( a ) === Person.prototype );      // 输出：true
```

&emsp;&emsp;目前我们一直在讨论“对象的原型”，就JavaScript的真正实现来说，其实并不能说对象有原型，而只能说对象的构造器有原型。对于“对象把请求委托给它自己的原型”这句话，更好的说法是对象把请求委托给它的构造器的原型。

&emsp;&emsp;JavaScript给对象提供了一个名为`__proto__`的隐藏属性，某个对象的`__proto__`属性默认会指向它的构造器的原型对象，即`{Constructor}.prototype`。所以`prototype`是函数的属性，不是实例对象的，实例对象拥有的是`__proto__`，用来查找`prototype`的。看到一张别人画的图，可以直观地了解原型链：

![prototype chain](https://images20200326.oss-cn-hangzhou.aliyuncs.com/blog/prototype_chain.jpeg)

&emsp;&emsp;上图可以看到，`prototype.constructor`指向的是构造器函数本身，改变这个指针并不能改变构造函数。实例对象本身没有`constructor`属性，你访问到的是原型链上的`prototype.constructor`。

&emsp;&emsp;函数本身也是对象，也具有`__proto__`，他指向的是JS内置对象`Function`的原型`Function.prototype`，所以你才能调用`fn.call`、`fn.apply`这些方法，你调用的其实是`Function.prototype.call`和`Function.prototype.apply`。

&emsp;&emsp;`prototype`本身也是对象，也具有`__proto__`，指向了他父级的`prototype`。`__proto__`和`prototype`的链式指向构成了JS的原型链。原型链的最终指向是`Object`，`Object`上面原型链是`null`，即`Object.__proto__ === null`。

