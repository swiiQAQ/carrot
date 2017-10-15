---
title: 关于this
date: 2017-10-13 14:05:47
tags:
---
上次提到的关于执行上下文中，执行上下文包括变量对象、作用域链和this
现在就研究研究this吧
在讲this之前先看看call和apply哈哈哈哈哈哈
## call()和apply()
>call()和apply()都是为了改变某个函数内的this的指向，call与apply的方法相似，区别只是call()方法接受的时若干参数的列表，而apply()接受的是一个包含多个参数的数组
call()
func.call(thisArg,arg1,arg2,...)
apply()
func.apply(thisArg,[arg1,arg2])

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
```
## this
> this的指向，是在函数被调用时确定的
>在非严格模式下，若this指向null或者undefined，则会自动指向全局对象（window对象）
