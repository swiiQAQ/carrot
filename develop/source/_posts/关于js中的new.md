---
title: 关于js中的new
date: 2017-10-17 14:00:53
tags:
---
刚开始我看到可以new一个函数的时候，我震惊了，对于我来说new是实例化类，js这种没有类的语言怎么可以new？？？
后来我发现一些很神奇的东西，甚至牵扯到了我一直没懂的原型链，下面就通过new来看看这些乱七八糟的东西吧
```HTML
function Panda(name,age){
    this.name = name;
    this.age = age;
}
Panda.prototype={
    id: 1,
}
var pd= new Panda('qiguo',3);
```
当时我就是看到类似这种东西的时候觉得什么情况？？？
然后网上说，new在js中的作用是什么呢？
```HTML
function newFunc(name,age){
    var temp = {};
    temp.__proto__ = Panda.prototype;
    Panda.call(temp,name,age);
    return temp;
}    
var pp = newFunc('qiyi',4);
```
这段代码的效果跟上面使用new是一样的，因为new的作用主要就是将实例出来的对象的__proto__指向原型Bar的prototype。这样子，每次实例化出的对象，都会具有Bar.prototype里面的方法和属性。并且只要改变Bar.prototype内的内容，所有实例的出的对象的属性也会发生变化。
那么为什么要使用new呢？
1、没有使用new的情况下，对于需要两个对象可以
```HTML
var pd1 = {
    name: 'qiguo',
    age: 3,
}
var pd2 = {
    name: 'qiyi',
    age: 4,
}
```
或者
```HTML
function Panda(name,age){
    return {
        name: name,
        age: age
    }
}
var pd1 = Panda('qiguo',3);
var pd2 = Panda('qiyi',4);
```
但是第一种情况下，明明是同一个结构每次写一遍，不好不好
第二种情况下，从外部看不出，pd1和pd2都是熊猫，不好不好
所以new 就派上用场了
```HTML
var Panda = function(name){
    this.name = name ;
    this.species = 'panda'
}
var pd1 = new Panda('qiguo');
var pd2 = new Panda('qiyi');
```
但是这样子的话，如果在后面要改变Panda的species的话，不能使所有的panda的species的值都发生变化。例如：
pd1.species = 'tiny panda';
pd2.species仍然是panda，
所以演变成了下面这种
```HTML
var Panda = function(name){
    this.name = name;
}
Panda.prototype ={
    species : 'panda'
}
var pd1 = new Panda('qiguo');
var pd2 = new Panda('qiyi');
```
如果突然要将panda的实例的species的属性改变的话，只需要
Panda.prototype.species = 'tiny panda'
那么pd1.species和pd2.species都会变成tiny panda
所以，对于共享的方法或者属性，是可以放在构造函数的prototype属性中，因为所有的实例的species属性指向的都是同一个内存地址，则改变所有引用该地址的值都发生变化。
而每个实例不同的属性则可以放在构造函数中，实例的时候在进行复写。
并且为了看出pd1和pd2同是出自于Panda构造函数，可以通过constructor属性判断
所以还需要Panda.prototype.constructor = Panda 来指向Panda，这样子pd1.constructor和pd2.constructor的值都为Panda。
所以JS是利用prototype原型链实现了正常面向对象语言的类的功能，利用new来进行实例化。

