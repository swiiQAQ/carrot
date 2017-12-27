---
title: JAVASCRIPT高级程序设计（一）
date: 2017-12-24 23:17:52
tags:
---
## 第二章 在HTML中使用JAVASCRIPT
### 2.1 < script >元素
async: 可选，表示立即下载脚本
defer: 可选，表示脚本可以延迟到文档完全被解析和显示之后再执行。
>但是延迟脚本并不一定会延迟顺序执行，也不一定会在DOMContentLoaded事件触发前执行，因此最好只包含一个延迟脚本。
defer属性只适用于外部脚本文件。
带有src属性的< script >元素不应该在其< script >和< /script >标签之间再包含额外的JavaScript代码

### 2.2 标签的位置
在< head >元素中包含所有JavaScript，意味着必须等到全部Javascript代码都被下载，解析和执行完成以后，才能开始呈现页面的内容（浏览器在遇到<body>标签时才开始呈现内容）
## 第三章 基本概念
### 3.1语法
#### 3.1.1 标识符
变量、函数、属性的名字，或者函数的参数。
第一个字符必须是一个字母、_、$，其他字符可以是字母、_、$或数字
#### 3.1.2严格模式
严格模式是ES5引入的概念，在严格模式下，一些不确定的行为将得到处理，而且对某些不安全的操作也会抛出错误
>ES6默认严格模式

### 3.2 变量
用var操作符定义的变量将成为定义该变量的作用域中的局部变量的作用域中的局部变量，即如果在函数中使用var定义一个变量，这个变量在函数退出后销毁。
但是如果在函数中没有使用var定义，会创建一个全局变量，在函数外部也可以访问到，但是并不建议这样。
### 3.4 数据类型
五种基本数据类型
Undefined
Null
Boolean
Number
String
一种复杂类型
Object（本质上是由一组无序的名值对组成的，function也属于Object类型）
#### 3.4.1 typeof操作符
返回值为下列字符串: undefined boolean string number object function

>typeof null //object null被认为是一个空的对象引用
safari5及之前，chrome7及之前的版本中 typeof regExp为function，其他浏览器返回object

#### 3.4.2 undefined类型
```HTML
var a;
typeof a    //undefined 没定义的值为undefined
typeof b    //undefined 虽然b连声明都没有声明，也是会返回undefined，但是如果直接使用b这个变量，会报错。
```

#### 3.4.3 null类型
>null == undefined  //true

#### 3.4.4 boolean类型
>boolean类型的值是区分大小写的，True和False并不是boolean值
所有的值都可以转换成boolean值

| 数据类型       | true          |  false   |
| ------------- |:-------------:| :-------------: |
| Boolean     | true |  false |
| String     | 非空字符串  |  "" |   
| Number    | 非零的数字   |    0和NAN    |
| Object    | 任何对象 |    null    |
| Undefined | -- | undefined | 

#### 3.4.5 Number类型
1、浮点数值
对于极大极小的数值，用e表示，表示的数值为e前面的数值乘以10的指数次幂
浮点熟知的最高精度是17位小数
>0.1+0.2 == 0.3 //false 浮点数值计算产生的舍入误差问题

2、数值范围
最小值被表示为Number.MIN_VALUE,即5e-324
最大值被表示为Number.MAX_VALUE,即1.7976931348623157e+308
如果超过最大值则为Infinity，小于最小值为-Infinity
想要确认是否为有穷数，可以用isFinite()函数判断，无穷数则为true

3、NaN
NaN的意思为Not a Number,用于表示一个本来要返回数值的操作数未返回数值的情况（避免抛出错误，代码就可以继续执行）
>NaN和任何的操作返回的都是NaN
NaN不和任何值相等，包括NaN本身，判断是否为数字可以用isNan()函数
isNaN()会将接收的值转换为数值例如"10"纯数字的字符串或者是boolean值，不能转换为数值的返回true
