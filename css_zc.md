# css

## 1.概念

- CSS: Cascading Style Sheet (层叠样式表)

- HTML   注重内容

- CSS      注重表现

- 基本语法

  ```
  selector {property: value}
  ```

## 2.三种选择器

- 标签选择器
- 类选择器
- ID选择器

```html
<head>
	<style type="text/css">
      	/*标签选择器*/
		h1 {
			color: red;
			font-family: "微软雅黑";
		}
      	/*ID选择器*/
		#testid01 {
			color: green;
			border: 1px solid black;
		}
      	/*class选择器*/
		.pclass {
			background-color: #ccc;
		}
	</style>
</head>
<body>
	<h1 id="titleId">七夕节快乐</h1>
	<p id="testid01">今天我很开心，为什么？</p>
	<p id="testid02" class="pclass">被一位基佬送了一朵玫瑰花</p>
	<div id="testid03" class="pclass">我是一只猴子</div>
</body>
```

## 3.三种范围

- 行内样式

  ```
  <p style="color:red;font-size:36px;font-weight:bold">我的心情</p>
  ```

- 页面样式

  ```
  <head>
      <style type="text/css">
      /* 标签选择器 */
      p {
        border: 1px solid lightgreen;
        color: #140;
      }
      /* 类选择器 */
      .c1 {
        background-color: #CCC;
      }
      /* ID选择器 */
      #i1 {
        text-shadow: 10px 10px 20px #963;
      }
      </style>
  </head>
  ```

- 全局样式

  - 把样式放置到样式表.css文件中
  - 在其它页面可以通过下面两个方式进入调用
    - 链接:`<link>`
    - 导入:@import

  ```
  <!-- 使用链接 -->
  <link rel="stylesheet" type="text/css" href="css/main.css">

  <!-- 使用导入 -->
  <style type="text/css">
    	@import url('css/main.css');
  </style>
  ```

## 4.优先级

- 3种选择器: ID选择器>class选择器>html选择器
- 3种样式:行内>页面>全局

## 5.复合选择器

### 5.1后代选择器

```
 body b {
        color: blue;
        text-decoration: line-through;
    }
 <b>问君能有几多愁</b>
<h3>恰似一江
	<b>春水</b>向东流。
</h3>
```
### 5.2直接子代选择器

```
 body>b {
        color: blue;
        text-decoration: line-through;
    }
 <b>问君能有几多愁</b>
<h3>恰似一江
	<b>春水</b>向东流。
</h3>
```
### 5.3交集选择器

```
/* 是p标签选择器且是txt的class选择器 */
p.txt {
color: #085;
}
/* 并集选择器 */
<p class="txt">
<b class="txt">不论你来自何方</b> 咱们都是中国人
</p>
```
### 5.4并集选择器

```
/* 并集选择器 */
h2,h5 {
color: #999;
}
<h2>h2标题</h2>
<h5>h5标题</h5>
```
### 5.5下一兄弟选择器

```
/*下一兄弟选择器*/
.item+li{
	background-color: #ccc;
}
```

## 6.样式是可以继承的

- 子标签可以继承父标签的样式风格
- 子标签的样式不会影响父标签的样式 
- color、 text-开头的、line-开头的、font-开头的。

```
<head>
	<style>
		ul>li {
			color: cyan;
			text-decoration: underline;
			line-height: 50px;
			font-family: "楷体";
			background-color: aliceblue;
			border: 1px solid red;
		}
	</style>
</head>
<body>
	<p>江苏万和</p>
	<ul>
		<li>
			java
			<ul>
				<span>java95</span>
				<li>java97</li>
				<li>java98</li>
				<li>java99</li>
			</ul>
		</li>
		<li>
			web
			<ul>
				<li>web01</li>
				<li>web02</li>
				<li>web03</li>
			</ul>
		</li>
	</ul>
</body>
```

## 7.常用样式

### 7.1字体样式

- font-style   样式 (normal | italic)
- font-weight 粗细(bold|700)
- font-size   字体大小，单位为px
- font-family: 字体

简写

- font:样式  粗细  大小  字体

```
.desc {
        /* font-style: italic;
        font-weight: bold;
        font-size: 38px;
        font-family: "华文琥珀"; */
        font: italic bold 48px "华文琥珀";
    }
<body>
    <div class="desc">
        美好的一天，快乐的一天，收获的一天
    </div>
</body>
```

### 7.2文本排版

- 规定元素中的文本的水平对齐方式。	text-align: left|center|right
- 属性设置元素的垂直对齐方式。   vertical-algin:top|middle|bottom
- 首行文字缩进  text-indent:2em;(1em=16px)
- 块标签的垂直对齐，设置  vertical-algin是无效的
- 块标签的垂直对齐，设置把块标签的line-height设置成块标签高度

```
.p1 {
  text-indent: 2em;
}
.p2 {
  text-align: center;
  line-height: 500px;
  border: 10px double red;
  height: 500px;
}
<p class="p1">1这是新闻报道时间：今天早上...</p>
<p class="p2">2这是新闻报道时间：今天早上...</p>
```

### 7.3边框

- 边框宽度  border-width

- 边框样式 border-style      dotted|dashed|solid|double

- 边框颜色 border-color

  简写

  border :   宽度  样式  颜色

```
.bor {
  /* border-width: 3px;
  border-style: dotted;
  border-color: blue;*/
 /* border: 3px dotted blue; */
  border-top: 3px dotted blue;
  border-right: 2px solid #F00;
  border-bottom: 4px dashed #0F0;
  border-left: 5px double #007;
}
<div class="bor">
  边框的样式学习
</div>
```

## 8.链接的样式

- 超链接有伪类样式: 如访问之前(a:link)、已经访问过(a:visited)、悬停时(a:hover)，点击时(a:active)
- 如果四种都写是要有顺序的: love   hate

```
<head>
	<style>
		a {
			text-decoration: none;
		}
		a:link {
			color: green;
		}
		a:visited {
			color: #000000;
		}
		a:hover {
			color: red;
		}
		a:active {
			color: yellow;
		}
	</style>
</head>
<body>
	<a href="index.html" target="_blank">这是一个连接</a>
</body>
```

## 9.背景颜色、背景图片与列表样式

- 背景颜色  background-color:
- 背景图片 background-image:url('路径')
- 背景重复 background-repeat : norepeat|repeat|repeat-x|rpeat-y
- 背景偏移 background-position : 左 上 
- 列表         list-style: none;

```
<head>
	<style>
		* {
			font-size: 14px;
		}
		#container {
			width: 1400px;
			border: 1px solid #f40;
			background-color: #ccc;
		}	
		.title {
			line-height: 400px;
			/*background-image: url("img/wzx.jpg");*/
			/*background-repeat: no-repeat;*/
			background: #FF0000 url("img/wzx.jpg") no-repeat 80px 10px;
			background-size: 1400px 400px;
		}
		ul,li {
			list-style: none;
		}
		ul a {
			text-decoration: none;
			font-size: 2em;
		}
	</style>
</head>
<body>
	<div id="container">
		<div class="title">全部商品分类</div>
		<ul>
			<li>
				<a href="#">图书</a>
				<a href="#">音像</a>
				<a href="#">数字商品</a>
			</li>
			<li>
				<a href="#">图书</a>
				<a href="#">音像</a>
				<a href="#">数字商品</a>
			</li>
		</ul>
	</div>
</body>
```

## 10.盒子模型

### 10.1.border

- border-width: 10px;  上下左右全为10px

  - border-width: 10px 20px 30px 40px; 上10 右20 下30 左40

- border-style:solid; 下下左右全为实线

  - border-style: solid dashed dotted double;  上实右虚下点左双

- border-color

  - border-color: red green blue yellow; 上red右green下blue左yellow

  - border-color: red green ; 上下red  左右green

  - border-color: red green blue;  上red  左右green 下blue

  - border-color:red 上右下左都为red

    上面写法相当于

  - border-top-color:red;

  - border-right-color:red;

  - border-bottom-color:red;

  - border-left-color:red;

  简写

  border:  width style color;

### 10.2margin外边距

- margin-top

- margin-right

- margin-bottom

- margin-left

  简写

  margin:10px 20px 30px  40px 上10右20下30左40

  margin:10px

- 作用二，可以设置行居中

  - margin:0px auto;

### 10.3padding内边距

- padding-top

- padding-right

- padding-bottom

- padding-left

  简写

  padding:10px 20px 30px 40px ; 

  padding:10px;

```
<head>
	<style>
		#container{
			border: 1px dashed red;
			height:  400px;
			width: 700px;
			margin: 0 auto;
		}
		.innerDiv{
			height: 300px;
			width: 500px;
			border: 1px solid  red;
			margin: 10px 20px 30px 40px;
			padding:  10px 20px 30px 40px;
			border-style: double solid  dotted dashed;  
			border-width: 2px 4px 6px 8px;
		}
	</style>
</head>
<body>
	<div id="container">
		<div class="innerDiv">
			王琦是班长~~
		</div>
	</div>
</body>
```

## 11.display属性

值有三种

- inline:同一行

- block:块

- none:隐藏(不占)

  区别：visibility:visiable|hidden：隐藏（占位置）

  内联样式与块样式 

  内联样式不占一行，比如`<a><b><span>`

  块样式独占一行，比如`<p><h1><div>`

脱标：内联样式与块样式进行互变（通过display属性），这种行为称为脱标。

```
<head>
	<style type="text/css">
		p{
			border: 1px solid red;
		}
		.container .p1{
			/*同一行*/
			display: inline;
		}
		.container>#span1{
			/*块*/
			display: block;
		}
		/*隐藏：不占位置*/
		.container .p2{
			display: none;
		}
		/*隐藏：占位置*/
		.container .p3{
			visibility: hidden;
		}
		/*display会导致脱标*/
	</style>
</head>
<body>
	<!--块：div;p;h1;ul...-->
	<!--行：a;img;font;i;b,span;lale;input-->		
	<div class="container">
		<span id="span1">
			我在左边
		</span>
		<span id="span2">
			我在右边
		</span>		
		<p class="p1">我是一个块级元素1</p>
		<p class="p2">我是一个块级元素2</p>
		<p class="p3">我是一个块级元素3</p>
		<p class="p4">我是一个块级元素4</p>
	</div>		
</body>
```

## 12.浮动(float)

- 三个值:
  - left: 往左浮动
  - right往右浮动
  - none 不浮动
- 清除浮动有四个值(clear)
  - left:清除左边的浮动
  - right:清除右边的浮动
  - both:清除两边的浮动
  - none:不清除浮动
- 清除浮动的作用
  - 脱标
  - 不会继续占着父容器
- 清除浮动四种方法
  - overflow:hidden;
  - clear:both;
  - 使用伪元素来清除浮动（面试的时候用）
  - 使用双伪元素清除浮动（面试的时候用）

```
<head>
	<style type="text/css">
		#container {
			border: 1px solid red;
			/*妙用overflow*/
			overflow: hidden;
		}
		#d1 {
			float: left;
			border: 1px solid green;
		}
		#d2 {
			float: left;
			border: 1px solid blue;
		}
		#d3 {
			float: right;
			border: 1px dashed orange;
		}	
		#d4 {
			clear: both;
		}
	</style>
</head>
<body>
	<div id="container">
		<div id="d1"><img src="img/photo-1.jpg" height="150" width="150" alt=""></div>
		<div id="d2"><img src="img/photo-2.jpg" height="150" width="150" alt=""></div>
		<div id="d3"><img src="img/photo-3.jpg" height="150" width="150" alt=""></div>
		<div id="d4">TM</div>
	</div>
</body>
```

## 13.float练习（黑色菜单条）

```
<head>
    <style type="text/css">
    #menu {
        margin: 0 auto;
        background-color: #000;
        height: 35px;
        width: 960px;
    }
    ul {
        list-style: none;
    }
    ul>li {
        float: left;
        line-height: 35px;
    }
    ul>li>a {
        text-decoration: none;
        font: normal bold 16px "黑体";
        color: #fff;
        padding: 10px 20px;
    }
    ul>li>a:hover {
        background-color: #f40;
    }
    /* 下一兄弟 */
    li+li {
        /* border-left: 1px dashed #fff; */
        background: url('img/forumMenuBg.gif') no-repeat 0px 2px;
    }
    </style>
</head>
<body>
    <div id="menu">
        <ul>
            <li><a href="#">首 页</a></li>
            <li><a href="#">知识库</a></li>
            <li><a href="#">论坛</a></li>
            <li><a href="#">学员问答</a></li>
            <li><a href="#">圈子</a></li>
            <li><a href="#">实时课堂</a></li>
            <li><a href="#">客户端下载</a></li>
            <li><a href="#">帮助中心</a></li>
        </ul>
    </div>
</body>
```

## 14.溢出处理(overflow)

有四个值:

- visible:默认，超过盒子，则显示盒子外
- hidden:超出则不显示
- scroll:超出显示滚动条
- auto:需要的时候显示滚动条

```
<head>
    <style type="text/css">
    div {
        border: 1px red solid;
        height: 200px;
        /* overflow: visible; */
        /* overflow: scroll; */
        /* overflow: auto; */
        overflow: hidden;
    }
    </style>
</head>
<body>
    <div>
        <img src="img/meinv.jpg" alt="">
    </div>
</body>
```

## 15.定位(postion)

有四个值:

- static		静态（默认值）
- relative          相对位置：相对它原来的位置（标准流）
- absolute        绝对位置(子绝父相)（绝定位）【脱标】  
- fixed              固定定位（浏览器兼容不好，用的很少）

```
<head>
	<style type="text/css">
		/* "*":通配符 */
		* {
			margin: 0px;
			border: 0px;
		}
		#contanier {
			border: 1px solid #0000ff;
			position: relative;
		}
		#contanier>div {
			border: 1px solid #ff0000;
			height: 80px;
		}
		/*定位position：*/
		/*1、static :默认值*/
		#contanier>.d1 {
			/*2、fixed固定定位: 固定浏览器,兼容性较差*/
			position: fixed;
			top: 50px;
			left: 30px;
		}
		#contanier>.d2 {
			/*3、relative相对的:相对原来的位置,不会脱标,占着空间*/
			position: relative;
			left: 10px;
			top: 30px
		}
		#contanier>.d3 {
			/*4、absolute绝对的；子绝父相，会脱标，不占空间*/
			/*1.绝对于最近的已定位祖先元素（relative）*/
			/*2.如果祖先元素没有定位，这绝对于html*/
			position: absolute;
			left: 20px;
			top: 50px;
		}
	</style>
</head>
<body>
	<div style="height: 200px;">
	</div>
	<div id="contanier">
		<div class="d1">div1</div>
		<div class="d2">div2</div>
		<div class="d3">div3</div>
		<div class="d4">div4</div>
	</div>
</body>
```













