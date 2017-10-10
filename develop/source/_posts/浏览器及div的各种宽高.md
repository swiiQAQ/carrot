---
title: 浏览器及div的各种宽高
date: 2017-08-24 16:38:23
tags:
---
### 浏览器视口宽高
#### js
``` HTML
window.innerWidth（包括滚动条宽度）
window.innerHeight（包括滚动条高度）
document.documentElement.clientWidth（不包括滚动条宽度）
document.documentElement.clientHeight（不包括滚动条高度）
```
### 整个页面的宽高，不包括滚动条宽高
#### js
``` HTML
document.body.clientWidth()
document.body.clientHeight()
```
#### JQUERY
``` HTML
$("body").width()
$("body").height()
```
### 浏览器的视口高度包括头上的选项卡地址栏的高度
#### js
``` HTML
window.outerWidth
window.outerHeight
```
![](/img/FirefoxInnerVsOuterHeight2.png) 