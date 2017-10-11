---
title: 大佬们研究的css黑魔法
date: 2017-09-29 14:42:59
tags:
---
<style>
.checkbox{
    display: inline-block;
    width: 15px;
    height: 15px;
    border: 1px solid green;
    text-align: center;
    line-height: normal;
}
.checkbox:after{
    content: "√";
    font-size: 12px;
    color: green;
}
.box div,.box span {
    display: inline-block;
    width: 200px;
    height: 30px;
    margin: 10px;
    border: 1px solid #333;
}
.box span:nth-of-type(2) {
    border: 1px solid red;
}
.radio-beauty-container {
    font-size: 0;
}
.radio-name {
    vertical-align: middle;
    font-size: 16px;
}
.radio-beauty {
    width: 18px;
    height: 18px;
    box-sizing: border-box;
    display: inline-block;
    border: 1px solid green;
    vertical-align: middle;
    margin: 0 15px 0 3px;
    border-radius: 50%;
}
.radio-beauty:hover {
    box-shadow: 0 0 7px green;
    padding: 2px;
    background-color: green;
    background-clip: content-box;
}
input[type="radio"]:checked+.radio-beauty {
    padding: 2px;
    background-color: green;
    background-clip: content-box;
}
</style>

## background-clip 背景的绘制区域（可用来画radio）
```HTML
.radio{
    display:inline-block;
    border-radius:50%;
    border:1px solid green;
    width:18px;
    height:18px;
    box-sizing:border-box;
    padding:5px;
    background:green;
    background-clip:content-box;
}
<label class="radio"></label>
```
<label style="display:inline-block;border-radius:50%;border:1px solid green;width:18px;height:18px;box-sizing:border-box;padding:5px;background:green;background-clip:content-box"></label>
## 利用after写checkbox
```HTML
.checkbox{
    display: inline-block;
    width: 12px;
    height: 12px;
    border: 1px solid green;
    text-align: center;
}
.checkbox:after{
    content: "√";
    font-size: 12px;
    color: green;
}
<label class="checkbox"></label>
```
<label class="checkbox"></label>
## 利用:checked和+选中美化后的radio
```HTML
.box div,.box span {
    display: block;
    width: 200px;
    height: 30px;
    margin: 10px;
    border: 1px solid #333;
}
.box span:nth-of-type(2) {
    border: 1px solid red;
}
.radio-beauty-container {
    font-size: 0;
}
.radio-name {
    vertical-align: middle;
    font-size: 16px;
}
.radio-beauty {
    width: 18px;
    height: 18px;
    box-sizing: border-box;
    display: inline-block;
    border: 1px solid green;
    vertical-align: middle;
    margin: 0 15px 0 3px;
    border-radius: 50%;
}
.radio-beauty:hover {
    box-shadow: 0 0 7px green;
    padding: 2px;
    background-color: green;
    background-clip: content-box;
}
input[type="radio"]:checked+.radio-beauty {
    padding: 2px;
    background-color: green;
    background-clip: content-box;
}
<div class="radio-beauty-container">
    <label>
        <span class="radio-name">HTML</span>
        <input type="radio" name="radioName" id="radioName1" hidden/>
        <label for="radioName1" class="radio-beauty"></label>
    </label>
    <label>
        <span class="radio-name">CSS</span>
        <input type="radio" name="radioName" id="radioName2" hidden/>
        <label for="radioName2" class="radio-beauty"></label>
    </label>
    <label>
        <span class="radio-name">Javascript</span>
        <input type="radio" name="radioName" id="radioName3" hidden/>
        <label for="radioName3" class="radio-beauty"></label>
    </label>
</div>
```
<div class="radio-beauty-container">
    <label>
        <span class="radio-name">HTML</span>
        <input type="radio" name="radioName" id="radioName1" hidden/>
        <label for="radioName1" class="radio-beauty"></label>
    </label>
    <label>
        <span class="radio-name">CSS</span>
        <input type="radio" name="radioName" id="radioName2" hidden/>
        <label for="radioName2" class="radio-beauty"></label>
    </label>
    <label>
        <span class="radio-name">Javascript</span>
        <input type="radio" name="radioName" id="radioName3" hidden/>
        <label for="radioName3" class="radio-beauty"></label>
    </label>
</div>