---
title: 关于js中的new
date: 2017-10-17 14:00:53
tags:
---
刚开始我看到可以new一个函数的时候，我震惊了，对于我来说new是实例化类，js这种没有类的语言怎么可以new？？？
后来我发现一些很神奇的东西，甚至牵扯到了我一直没懂的原型链，下面就通过new来看看这些乱七八糟的东西吧
```HTML
function Bar(){
    var a = 0;
}
Bar.prototype={
    init:function(){
        console.log('init');
    },
    color: 'blue'
}
var bar = new Bar();
```
当时我就是看到类似这种东西的时候觉得什么情况？？？
然后网上说，new在js中的作用是什么呢？
```HTML
function Bar(){
    var a = 0;
}
function newFunc(){
    var temp = {};
    temp.__proto__ = Bar.prototype;
    Bar.call(temp);
    return temp;
}
var bar = newFunc();
```
这段代码的效果跟上面使用new是一样的，因为new的作用主要就是将实例出来的对象的__proto__指向原型Bar的prototype。这样子，每次实例化出的对象，都会具有Bar.prototype里面的方法和属性。并且只要改变Bar.prototype内的内容，所有实例的出的对象的属性也会发生变化
