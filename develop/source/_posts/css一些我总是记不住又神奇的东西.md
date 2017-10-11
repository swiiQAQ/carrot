---
title: css一些我总是记不住又神奇的东西
date: 2017-09-29 15:00:31
tags:
---
# text-shadow
</br>
>text-shadow: x-shadow y-shadow blur color;

```HTML
    <h1 style="color:white;text-shadow:2px 2px 4px #000000;">白色文本的阴影效果！</h1>
```
<h1 style="color:white;text-shadow:2px 2px 4px #000000;">白色文本的阴影效果！</h1>
```HTML
<div style="background:#666;width:200px">
    <h1 style="color: #eee;text-shadow: 6px 6px 0 #666, 7px 7px 0 #eee;">VINTAGE RETRO</h1>
</div>
```
<div style="background:#666;width:200px">
    <h1 style="color: #eee;text-shadow: 6px 6px 0 #666, 7px 7px 0 #eee;">VINTAGE RETRO</h1>
</div>

```HTML
<div style="background:#666">
    <h1 style="color: transparent;text-shadow:0 0 6px #F96, -1px -1px  #FFF, 1px -1px  #444">World</h1>
</div>
```
<div style="background:#666">
    <h1 style="color: transparent;text-shadow:0 0 6px #F96, -1px -1px  #FFF, 1px -1px  #444">World</h1>
</div>
<br/>
# box-shadow
</br>

>box-shadow:inset x-shadow y-shadow blur spread color ;
x-shadow: 水平阴影的位置(required)；
y-shadow: 垂直阴影的位置(required)；
blur: 模糊距离；
spread: 阴影的尺寸；
color： 阴影的颜色(mz和opera缺省下为黑色，webkit为透明)；
inset/outset：内部阴影/外部阴影(缺省默认)；

# nth-child()和nth-of-type()的区别
</br>

### 不规定子元素的类型的情况下
>选择器和冒号之间隔一个空格的话，表示选择器下的任意子元素

```HTML
.box :nth-child(2){
    border: 1px solid red;
}
<div class="box">
    <div></div>
    <div></div>
    <span></span>
    <span></span>
</div>
```
![](/img/nth2.png '.box选择器下第二个子元素')
```HTML
.box :nth-of-type(2){
    border: 1px solid red;
}
<div class="box">
    <div></div>
    <div></div>
    <span></span>
    <span></span>
</div>
```
![](/img/nth1.png '.box选择器下任意同一标签的第二个子元素(div标签的第二个和span标签的第二个)')
### 规定子元素的类型的情况下
#### 规定类型为class的情况下
```HTML
.box .divItem:nth-child(2){
    border: 1px solid red;
}
<div class="box">
    <div class="divItem"></div>
    <div></div>
    <span class="divItem"></span>
    <span></span>
</div>
```
![](/img/nth3.png '因为第二个子元素class不是divItem，所以不对应任何元素')
```HTML
.box .divItem:nth-of-type(2){
    border: 1px solid red;
}
<div class="box">
    <span class="divItem"></span>
    <div class="divItem"></div>
    <div class="divItem"></div>
    <span class="divItem"></span>
    <span></span>
</div>
```
![](/img/nth4.png '选取的是span标签并且class为divItem的和div标签并且class为divItem的第二个元素')

#### 规定类型为标签名的情况下
```HTML
.box span:nth-child(2){
    border: 1px solid red;
}
<div class="box">
    <span class="divItem"></span>
    <div class="divItem"></div>
    <div class="divItem"></div>
    <span class="divItem"></span>
    <span></span>
</div>
```
![](/img/nth5.png '.box下第二个子元素的标签不是span所以匹配不上')
```HTML
.box span:nth-of-type(2){
    border: 1px solid red;
}
<div class="box">
    <span class="divItem"></span>
    <div class="divItem"></div>
    <div class="divItem"></div>
    <span class="divItem"></span>
    <span></span>
</div>
```
![](/img/nth6.png '.box下的第二个span元素')

# 选择器
## ~
eg: p~ul
为所有相同的父元素中位于 p 元素之后的所有 ul 元素设置背景
## +
选择相邻兄弟




