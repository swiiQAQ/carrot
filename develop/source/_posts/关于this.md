---
title: 关于this
date: 2017-10-13 14:05:47
tags:
---
上次提到的关于执行上下文中，执行上下文包括变量对象、作用域链和this
现在就研究研究this吧

## this
> this的指向，是在函数被调用时确定的
如果调用的函数是在某个对象中的，则函数中的this指向该对象
如果函数是独立存在的，函数中的this指向的是undefined（严格模式下）
在非严格模式下，若this指向null或者undefined，则会自动指向全局对象（window对象）

![](/img/this1.png '在严格模式下，this不存在')
![](/img/this2.png '非严格模式下，this指向了window')
![](/img/this3.png '函数独立调用，this是undefined，函数在对象中被调用，this指向对象（在这里是window）') 

![](/img/this4.png)

foo()单独调用在严格模式下应该是获取不到this，在这里非严格模式下，取到的是window.a为20
window.foo()在window对象中调用，this指向window，this.a即20
boo利用call将this指向了boo对象，所以this.a为boo.a即8

![](/img/this5.png)

fn和c里面的this是不一样的，因为fn里面的this是包含在fn函数中，fn函数是属于obj对象中的，所以在fn中的this指向的是obj，而C在{}中并没有形成新的作用域，所以c中的this指向的还是foo，但是因为foo函数是单独调用的，所以不存在this

## call()和apply()
>call()和apply()都是为了改变某个函数内的this的指向，call与apply的方法相似，区别只是call()方法接受的时若干参数的列表，而apply()接受的是一个包含多个参数的数组

call()  
func.call(thisArg,arg1,arg2,...)
apply()  
func.apply(thisArg,[arg1,arg2])

1、利用call，apply实现继承，将this的上下文变成在teacher中的上下文，复用了方法。
```HTML
var Person = function(){
}
Person.prototype={
    words: 'hello',
    say: function(){
        console.log(this.words);
    }
}
var teacher = new Person();
teacher.say();
var coders = {
	words: 'hello world',
}
teacher.say.call(coders)
//等同于Person.prototype.say.call(coders)
```

2、利用call做继承
```HTML
    var school = function(){
        this.degree = 'graduate degree';
        this.schoolName = 'jxnu'
    }
    var teacher = {
        name : 'teacher'
    }

    school.call(teacher);   
    //teacher: {name:'teacher',degree:'graduate degree',schoolName:'jxnu'}
```

3、call和apply的用法区别以及如何使用参数
```HTML
function add(a,b){
  return a+b;  
}
function sub(a,b){
  return a-b;  
}
var a1 = add.apply(sub,[4,2]);　　//sub调用add的方法
// var a1 = add.call(sub,4,2);   //等同于用apply
var a2 = sub.apply(add,[4,2]);
// var a2 = sub.apply(add,4,2);
alert(a1);  //6     
alert(a2);  //2
```