---
title: css布局整理
date: 2017-08-17 10:35:24
tags:
---
## 一、关于margin负边距的问题
### 1、负边距解释
通过margin负边距调整的位置和position：relative属性后调整位置不同，通过margin改变的位置后，后面的文档流会跟上，但是文档流只能是后面的流向前面的，即文档流只能向左或向上流动，不能向下或向右移动。
### 2、负边距具体例子
#### 1)通过负边距增加div宽度


```HTML
	
	<style>
		.box{
			width: 100px;
			height: 100px;
			margin: 0 auto;
		}
		.inner_box{
			height: 100px;
			margin-left: -50px;
			margin-light: -50px;
			background: #95E1D3;
		}
	</style>
	<div class = "box">
		<div class="inner_box">
		</div>
	</div>
```
![](/img/addWidth.png)

这种情况需要外面的盒子固定宽高，并且左右有空出的位置，否则看不出增加了宽度，
内部盒子需要不定宽，因为定宽后，margin-left会使得整个div像左偏移50px，而不会增加宽度。
#### 2）通过负边距调整类似商品列表布局的边距
```HTML
	<style>
		.box_wrap{
			width: 580px;
			height: 120px;
			border: 1px solid #95E1D3;
		}
		.item_box{
			margin-left: -10px;
			margin-right: -10px;
		}
		.item_box .item{
			float:left;
			width: 100px;
			height: 100px;
			background: #95E1D3;
			margin: 10px;
		}
	</style>
	<div class="box_wrap">
		<div class="item_box">
			<div class="item"></div>
			<div class="item"></div>
			<div class="item"></div>
			<div class="item"></div>
			<div class="item"></div>
		</div>
	</div>
```
![](/img/boxItem.png)
## 二、三列布局
### 1、流体布局
```HTML
<style>
	.left,.right,.middle{
		height: 500px;
	}
	.left{
		float: left;
		width: 200px;
		background: #F38181;
	}
	.right{
		float: right;
		width: 200px;
		background: #FCE38A;
	}
	.middle{
		margin-left: 200px;
		margin-right: 200px;
		background: #95E1D3;
	}
</style>
<body>
	<div class="left"></div>
	<div class="right"></div>
	<div class="middle"></div>
</body>
```
左列左浮动，右列又浮动，中间通过margin将左右两边的位置空出来，中间宽度自适应。
### 2、BFC布局
#### 1）BFC是什么
BFC(Block formatting context)直译为"块级格式化上下文"。它是一个独立的渲染区域，只有Block-level box参与， 它规定了内部的Block-level Box如何布局，并且与这个区域外部毫不相干。
#### 2)哪些元素触发BFC
根元素
float属性不为none
position为absolute或fixed
display为inline-block, table-cell, table-caption, flex, inline-flex
overflow不为visible
#### 3）BFC布局规则
内部的Box会在垂直方向，一个接一个地放置。
Box垂直方向的距离由margin决定。属于同一个BFC的两个相邻Box的margin会发生重叠
每个元素的margin box的左边， 与包含块border box的左边相接触(对于从左往右的格式化，否则相反)。即使存在浮动也是如此。
BFC的区域不会与float box重叠。
BFC就是页面上的一个隔离的独立容器，容器里面的子元素不会影响到外面的元素。反之也如此。
计算BFC的高度时，浮动元素也参与计算
#### 4）BFC三列布局
```HTML
<style>
	.left,.right,.middle{
		height: 500px;
	}           
	.left{
		float: left;
		width: 200px;
		background: #F38181;
	}
	.right{
		float: right;
		width: 200px;
		background: #FCE38A;
	}
	.middle{
		overflow: hidden;
		background: #95E1D3;
	}
</style>
<body>
	<div class="left"></div>
	<div class="right">	</div>
	<div class="middle"></div>
</body>
```
通过overflow：hidden产生BFC，因为BFC的区域不会与float box重叠，所以可以做到margin-left和margin-right的效果。
### 3、双飞翼布局
```HTML
	<style>
		.left,.right,.main{
			height: 500px;
			position: relative;
		}
		.content {
			float: left;
			width: 100%;
		}
		.main {
			margin: 0 200px;
			background: #95E1D3;
		}
		.left {
			float: left;
			width: 200px;
			margin-left: -100%;
			background: #F38181;
		}
		.right {
			width: 200px;
			float: right;
			margin-left: -200px;
			background: #FCE38A;
		}
	</style>
	<body>
		<div class="content">
			<div class="main"></div>
		</div>
		<div class="left"></div>
		<div class="right"></div>
	</body>
```
### 4、圣杯布局
```HTML
<style>
	.outbox{
		padding: 0 200px;
	}
	.left,.right,.middle{
		height: 500px;
		text-align: center;
	} 
	.middle{
		width: 100%;
		background: #95E1D3;
		float: left;
	}
	.left{
		float: left;
		width: 200px;
		margin-left: -100%;
		background: #F38181;
		position: relative;
		left: -200px;
	}
	.right{
		float: left;
		width: 200px;
		margin-left: -200px;
		background: #FCE38A;
		position: relative;
		right: -200px;
	} 
</style>
<body>
	<div class="outbox">
		<div class="middle"></div>
		<div class="left"></div>
		<div class="right"></div>
	</div>
</body>
```
圣杯布局和双飞翼布局的区别就是，双飞翼布局使用的是margin空开左右列的位置，而圣杯布局用的是padding，再用左右两列左右各移动200。
圣杯布局div结构更明了，但是样式较双飞翼更多一些。
一般要优先加载中间的内容会选择这两种布局。
### 5、flex布局
```HTML
<style>
	.container{
		display: flex;
	}
	.middle,.left,.right{
		height: 500px;
	}
	.middle{
		flex-grow: 1;
		background: #95E1D3
	}
	.left{
		order: -1;
		flex: 0 1 200px;
		background: #F38181                
	}
	.right{
		flex: 0 1 200px;
		background: #FCE38A
	}
</style>
<body>
	<div class="container">
		<div class="middle"></div>
		<div class="left"></div>
		<div class="right"></div>
	</div>
</body>
```
order: 定义项目在容器中的排列顺序，数值越小，排列越靠前，默认值为 0
flex: flex-grow, flex-shrink 和 flex-basis的简写
flex-grow: 定义项目的放大比例，默认为0.
flex-shrink: 定义了项目的缩小比例，默认为1.
flex-basis: 定义了在分配多余空间之前，项目占据的主轴空间,默认auto.
先通过order:-1将left排列在前面，这样就可以虽然是先加载middle，但left排前面。
再通过设置左右列在页面放大时，仍保持200px，但是middle在放大时会跟着放大，做到左右固定宽度，中间自适应。
## 三、多行文本垂直居中
### 1、通过display:table居中
```HTML
<style>
	.outBox{
		width: 100px;
		height: 100px;
        margin: 0 auto;
        background: #E9E9E5;
		display:table;
	}
	.innerBox{
		display: table-cell;
		vertical-align: middle;
        text-align: center;
	}
</style>
<body>
	<div class="outBox">
		<div class="innerBox">
			<p>middle</p>
			<p>middle</p>
		</div>
	</div>
</body>
```
### 2、通过transform居中(同样适用于div垂直居中)
```HTML
<style>
	.outBox2{
        width: 130px;
        height: 130px;
        background: #D4D6C8;
        position: relative;
        margin: 20px auto;
    }
    .innerBox2{
        position: absolute;
        top: 50%;
        left: 50%;
        transform: translate(-50%,-50%);
    }
</style>
<body>
    <div class="outBox2">
        <div class="innerBox2">
            <p>middle</p>
            <p>middle</p>
        </div>
    </div>
</body>
```

## 四、div垂直水平居中
### 1、同多行文本垂直水平居中一样，通过transform实现，此种情况可以不定宽不定高并且属于相对定位
这里不再赘述
### 2、根据绝对定位垂直水平居中
```HTML
<style>
	.centerBox,{
		width: 100%;
		height: 200px;
		position: relative;
	}
	.inlineBox {
		width: 100px;
		height: 100px;
		margin: auto;
		position: absolute;
		top: 0;
		left: 0;
		bottom: 0;
		right: 0;
		background: #009378
	}
</style>
<body>
	<div class="centerBox">
		<div class="inlineBox"></div>
	</div>
</body>
```
### 3、定宽，绝对定位
```html
<style>
	.centerBox,{
		position: relative;
	}
	.inlineBox2{
		width: 100px;
		height: 100px;
		position: relative;
		left: 50%;
		top: 50%;
		transform: translate(-50%,-50%); 
		background: #1EE494;
	}
</style>
<body>
	<div class="centerBox">
		<div class="inlineBox2"></div>
	</div>
</body>
```
