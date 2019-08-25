# Bootstrap入门

简介：

​	Bootstrap，来自 Twitter，是目前很受欢迎的前端框架。Bootstrap 是基于 HTML、CSS、JAVASCRIPT 的，它简洁灵活，使得 Web 开发更加快捷。[1][ ]() 它由Twitter的设计师Mark Otto和Jacob Thornton合作开发，是一个CSS/HTML框架。Bootstrap提供了优雅的HTML和CSS规范，它即是由动态CSS语言[Less](https://baike.baidu.com/item/Less)写成。

#1. 下载Bootstrap 

打开官方网址 [http://getbootstrap.com/](http://getbootstrap.com/) 进行下载。

也打开中文官网地址http://www.bootcss.com/ 进行下载

![img](http://images2015.cnblogs.com/blog/940966/201609/940966-20160902173035293-209952173.png)

准备项目模板文件夹

# 2. 加入Bootstrap

把Bootstrap源码包中的dist内容解压添加到项目结构中，因为Bootstrap需要jquery的支持，所以再加上jquery的支持

![img](http://upload-images.jianshu.io/upload_images/5350300-5c1f5747de7a4a03.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

# 3. 起步

```html
<!--HTML5 文档类型声明：-->
<!DOCTYPE html>
<html lang="zh-CN">
<head>
  	<!--页面的编码格式-->
	<meta charset="utf-8">
	<!--当IE浏览器以最新的引擎来渲染页面-->
	<meta http-equiv="X-UA-Compatible" content="IE=edge">
	<!--视口、移动端适配:适应我的设别宽度、100%缩放-->
	<meta name="viewport" content="width=device-width, initial-scale=1">
	<title>Bootstrap入门</title>
	<!-- Bootstrap样式库 -->
	<link href="bootstrap/css/bootstrap.css" rel="stylesheet">
	<!-- 如果ie版本低于IE9，html5shiv.min.js让其支持HTML5标签 ，respond.min.js让其支持响应式（媒体查询 ）-->
	<!--[if lt IE 9]>
	     <script src="http://cdn.bootcss.com/html5shiv/3.7.2/html5shiv.min.js"></script>
	     <script src="http://cdn.bootcss.com/respond.js/1.4.2/respond.min.js"></script>
    <![endif]-->
</head>
<body>
    <h1>你好，世界！</h1>
	<!-- jquery的核心js -->
	<script type="text/javascript" src="js/jquery-3.2.1.js"></script>
	<!-- bootstrap的核心js -->
	<script type="text/javascript" src="bootstrap/js/bootstrap.js"></script>
</body>
</html>
```

# 4. 全局CSS样式 

## 4.1. 布局容器 

`.container` 类用于固定宽度并支持响应式布局的容器。

`.container-fluid` 类用于 100% 宽度，占据全部视口（viewport）的容器。

```html
<!--没有使用响应式布局、正常操作-->
<div>
  好好学习，天天向上...
</div>
<!--固定宽度并支持响应式布局。-->
<div class="container">
  好好学习，天天向上...
</div>
<!--100% 宽度，占据全部视口（viewport）的容器-->
<div class="container-fluid">
  好好学习，天天向上...
</div>
```

## 4.2. 栅格系统 

- 必须放置在布置容器中
- 栅格参数

|                   | 超小屏幕 手机 (<768px)   | 小屏幕 平板 (≥768px)            | 中等屏幕 桌面显示器 (≥992px) | 大屏幕 大桌面显示器 (≥1200px) |
| ----------------- | ------------------ | -------------------------- | ------------------- | -------------------- |
| 栅格系统行为            | 总是水平排列             | 开始是堆叠在一起的，当大于这些阈值时将变为水平排列C |                     |                      |
| `.container` 最大宽度 | None （自动）          | 750px                      | 970px               | 1170px               |
| 类前缀               | `.col-xs-`         | `.col-sm-`                 | `.col-md-`          | `.col-lg-`           |
| 列（column）数        | 12                 |                            |                     |                      |
| 最大列（column）宽      | 自动                 | ~62px                      | ~81px               | ~97px                |
| 槽（gutter）宽        | 30px （每列左右均有 15px） |                            |                     |                      |
| 可嵌套               | 是                  |                            |                     |                      |
| 偏移（Offsets）       | 是                  |                            |                     |                      |
| 列排序               | 是                  |                            |                     |                      |

```html
<head>
    <meta charset="UTF-8">
  	<meta http-equiv="X-UA-Compatible" content="IE=edge">
  	<meta name="viewport" content="width=device-width, initial-scale=1">
  	<title></title>
 	<link href="bootstrap/css/bootstrap.css" rel="stylesheet">
  	<style type="text/css">
      div {
      	border: 1px solid red;
      }
  	</style>
</head>
<body>
  <div class="container">
    <div class="row">
      <div class="col-md-1">.col-md-1</div>
      <div class="col-md-1">.col-md-1</div>
      <div class="col-md-1">.col-md-1</div>
      <div class="col-md-1">.col-md-1</div>
      <div class="col-md-1">.col-md-1</div>
      <div class="col-md-1">.col-md-1</div>
      <div class="col-md-1">.col-md-1</div>
      <div class="col-md-1">.col-md-1</div>
      <div class="col-md-1">.col-md-1</div>
      <div class="col-md-1">.col-md-1</div>
      <div class="col-md-1">.col-md-1</div>
      <div class="col-md-1">.col-md-1</div>
    </div>
    <div class="row">
      <div class="col-md-8">.col-md-8</div>
      <div class="col-md-4">.col-md-4</div>
    </div>
    <div class="row">
      <div class="col-md-4">.col-md-4</div>
      <div class="col-md-4">.col-md-4</div>
      <div class="col-md-4">.col-md-4</div>
    </div>
    <div class="row">
      <div class="col-md-6">.col-md-6</div>
      <div class="col-md-6">.col-md-6</div>
    </div>
  </div>
  <hr/>
  <div class="container-fluid">
    <div class="row">
      <div class="col-md-1">.col-md-1</div>
      <div class="col-md-1">.col-md-1</div>
      <div class="col-md-1">.col-md-1</div>
      <div class="col-md-1">.col-md-1</div>
      <div class="col-md-1">.col-md-1</div>
      <div class="col-md-1">.col-md-1</div>
      <div class="col-md-1">.col-md-1</div>
      <div class="col-md-1">.col-md-1</div>
      <div class="col-md-1">.col-md-1</div>
      <div class="col-md-1">.col-md-1</div>
      <div class="col-md-1">.col-md-1</div>
      <div class="col-md-1">.col-md-1</div>
    </div>
    <div class="row">
      <div class="col-md-8">.col-md-8</div>
      <div class="col-md-4">.col-md-4</div>
    </div>
    <div class="row">
      <div class="col-md-4">.col-md-4</div>
      <div class="col-md-4">.col-md-4</div>
      <div class="col-md-4">.col-md-4</div>
    </div>
    <div class="row">
      <div class="col-md-6">.col-md-6</div>
      <div class="col-md-6">.col-md-6</div>
    </div>
  </div>
  <hr/>
  <div class="container">
    <div class="row">
      <div class="col-xs-12 col-md-8">.col-xs-12 .col-md-8</div>
      <div class="col-xs-6 col-md-4">.col-xs-6 .col-md-4</div>
    </div>
  </div>
</body>
```

## 4.3. 列偏移、列排序、列嵌套 

- 列偏移,只能往右

  ```
  col-md-offset-*
  ```

- 列排序 

  ```
  col-md-push-*和col-md-pull-*
  ```

- 列嵌套

  ```html
  <head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <title></title>
    <link href="bootstrap/css/bootstrap.css" rel="stylesheet">
    <style type="text/css">
      .row div {
        border: 1px solid red;
      }
    </style>
  </head>
  <body>
    <div class="container">
      <!--列偏移：col-md-offset-4,只能右移-->
      <div class="row">
        <div class="col-md-4 col-md-offset-4">.col-md-4</div>
        <div class="col-md-4 ">.col-md-4</div>
      </div>
      <div class="row">
        <div class="col-md-4 ">.col-md-4</div>
        <div class="col-md-4 col-md-offset-4">.col-md-4</div>
      </div>
      <!--列排序：col-md-push-* 和 col-md-pull-*-->
      <div class="row">
        <div class="col-md-4 col-md-push-4">.col-md-41</div>
        <div class="col-md-4  col-md-pull-4">.col-md-42</div>
      </div>
      <!--嵌套列：-->
      <div class="row">
        <div class="col-md-6 ">
          <div class="row">
            <div class="col-md-3">1</div>
            <div class="col-md-3">2</div>
            <div class="col-md-3">3</div>
            <div class="col-md-3">4</div>
          </div>
        </div>
        <div class="col-md-6 ">.col-md-42</div>
      </div>
    </div>
  </body>
  ```

## 4.4. 排版 

### 4.4.1.标题

HTML 中的所有标题标签，`<h1>` 到 `<h6>` 均可使用。另外，还提供了 `.h1` 到 `.h6` 类，为的是给内联（inline）属性的文本赋予标题的样式。在标题内还可以包含 `<small>` 标签。

```html
<h1>h1. Bootstrap heading <small class="h1">Secondary text</small></h1>
<h2>h2. Bootstrap heading <small>Secondary text</small></h2>
<h3>h3. Bootstrap heading <small>Secondary text</small></h3>
<h4>h4. Bootstrap heading <small>Secondary text</small></h4>
<h5>h5. Bootstrap heading <small>Secondary text</small></h5>
<h6>h6. Bootstrap heading <small>Secondary text</small></h6>
<hr>
```

### 4.4.2. 页面主体

全局 `font-size` 设置为 14px

`line-height` 设置为 1.42857143

`<p>` （段落）元素还被设置了等于 1/2 行高（即 10px）的底部外边距（margin）

### 4.4.3. 中心内容

通过添加 `.lead` 类可以让段落突出显示。

### 4.4.4.内联文本元素

- mark标签 

- delete标签 

  - 对于被删除的文本使用 `<del>` 标签。

- 无用标签 

  - 对于没用的文本使用 `<s>` 标签

- 插件标签 

  - 额外插入的文本使用 `<ins>` 标签

- 带下划线的文本

  - 为文本添加下划线，使用 `<u>` 标签

- 小号文本

  - 对于不需要强调的inline或block类型的文本，使用 `<small>` 标签包裹，其内的文本将被设置为父容器字体大小的 85%。标题元素中嵌套的 `<small>` 元素被设置不同的 `font-size` 。
  - 你还可以为行内元素赋予 `.small` 类以代替任何 `<small>` 元素。

- 着重

  - 通过增加 strong 值强调一段文本
  - <b>用于高亮单词或短语，不带有任何着重的意味</b>

- 斜体

  - 用斜体`<em>`调一段文本
  - 在 HTML5 中可以放心使用 `<b>` 和 `<i>` 标签。`<b>` 用于高亮单词或短语，不带有任何着重的意味；而 `<i>` 标签主要用于发言、技术词汇等

  ```html
  <span>普通文本</span>
  <mark>标记文本</mark>
  <del>被删除的文本</del>
  <s>无用文本</s>
  <ins>插入的文本</ins>
  <u>带下划线的文本</u>
  <br>
  <small>小号文本</small>
  <span class="small">小号文本</span>
  <strong>着重</strong>
  <em>斜体</em>
  <b>用于高亮单词或短语，不带有任何着重的意味</b>
  <i>主要用于发言、技术词汇等</i>
  <hr>
  ```

- 对齐

  ```html
  <p class="text-left">左对齐</p>
  <p class="text-right">右对齐</p>
  <p class="text-center">居中对齐</p>
  <p class="text-justify">两端对齐</p>
  <p class="text-nowrap" style="width:30px; border:1px solid red">超出后不换行</p>
  <hr>
  ```

- 改变大小写

  ```html
  <p class="text-lowercase">WANho万和</p>
  <p class="text-uppercase">WANho万和</p>
  <!--首字母大写-->
  <p class="text-capitalize">welCome to wanho万和</p>
  <hr>
  ```

- 列表

  ```
  <ul class="list-unstyled list-inline">
    <li>1</li>
    <li>2</li>
    <li>3</li>
  </ul>
  ```

- 描述

  - `.dl-horizontal` 可以让 `<dl>` 内的短语及其描述排在一行。开始是像 `<dl>` 的默认样式堆叠在一起，随着导航条逐渐展开而排列在一行。

  ```
  <dl class="dl-horizontal">
    <dt>标题1</dt>
    <dd>描述1...</dd>
    <dt>标题1</dt>
    <dd>描述1...</dd>
  </dl>
  ```

## 4.5. 代码  

### 4.5.1. 内联代码 

- 通过 `<code>` 标签包裹内联样式的代码片段。

### 4.5.2. 用户输入 

- 通过 `<kbd>` 标签标记用户通过键盘输入的内容。

### 4.5.3. 代码块 

- 多行代码可以使用 `<pre>` 标签。为了正确的展示代码，注意将尖括号做转义处理。

### 4.5.4. 变量 

- 通过 `<var>` 标签标记变量。

### 4.5.5. 程序输出 

- 通过 `<samp>` 标签来标记程序输出的内容。

```html
<div class="container">
  	<span>我是最棒的~</span>
  	<code>我是最棒的~</code>
    <br/>
  	<!--需要转译-->
  	<code>我是最棒的<String></code>
    <code>我是最棒的&lt;String&gt;</code>
    <br/>
    <!--键盘按下-->
    To switch directories, type <kbd>cd</kbd> followed by the name of the directory.<br> To edit settings, press <kbd><kbd>ctrl</kbd> + <kbd>,</kbd></kbd>
 </div>
```

## 4.6. 表格 

### 4.6.1. 基本实例 

- 为任意 `<table>` 标签添加 `.table` 类可以为其赋予基本的样式 

### 4.6.2. 条纹状表格 

- 通过 `.table-striped` 类可以给 `<tbody>` 之内的每一行增加斑马条纹样式。

### 4.6.3. 带边框的表格 

- 添加 `.table-bordered` 类为表格和其中的每个单元格增加边框。

### 4.6.4. 鼠标悬停 

- 通过添加 `.table-hover` 类可以让 `<tbody>` 中的每一行对鼠标悬停状态作出响应。

### 4.6.5. 紧缩表格 

- 通过添加 `.table-condensed` 类可以让表格更加紧凑，单元格中的内补（padding）均会减半。

### 4.6.6. 状态类 

- 通过这些状态类可以为行或单元格设置颜色。

| Class      | 描述                 |
| ---------- | ------------------ |
| `.active`  | 鼠标悬停在行或单元格上时所设置的颜色 |
| `.success` | 标识成功或积极的动作         |
| `.info`    | 标识普通的提示信息或动作       |
| `.warning` | 标识警告或需要用户注意        |
| `.danger`  | 标识危险或潜在的带来负面影响的动作  |

### 4.6.7. 响应式表格 

- 将任何 `.table` 元素包裹在 `.table-responsive` 元素内，即可创建响应式表格，其会在小屏幕设备上（小于768px）水平滚动。当屏幕大于 768px 宽度时，水平滚动条消失。

```html
<div class="container">
		<table class="table table-hover ">
			<thead>
				<tr class="active">
					<th>学号</th>
					<th>姓名</th>
				</tr>
			</thead>
			<tbody>
				<tr class="danger">
					<td>1001</td>
					<td>张三</td>
				</tr>
				<tr class="info">
					<td>1002</td>
					<td>李四</td>
				</tr>
				<tr class="success">
					<td>1003</td>
					<td>王五</td>
				</tr>
				<tr class="warning">
					<td>1004</td>
					<td>赵六</td>
				</tr>
			</tbody>
		</table>
</div>
```

## 4.7. 表单 

### 4.7.1. 基本实例 

- 单独的表单控件会被自动赋予一些全局样式。所有设置了 `.form-control` 类的 `<input>`、`<textarea>` 和 `<select>` 元素都将被默认设置宽度属性为 `width: 100%;`。 将 `label` 元素和前面提到的控件包裹在 `.form-group` 中可以获得最好的排列。

  ```html
  <!--表单的基本实例-->
  <form>
  	<div class="form-group">
  		<label for="username">用户名</label>
  		<input type="text" class="form-control" name="username" id="username" placeholder="请输入用户名" />
  	</div>
  	<div class="form-group">
  		<label for="password">密码</label>
  		<input type="password" class="form-control" name="password" id="password" placeholder="请输入密码" />
  	</div>
  </form>
  ```

### 4.7.2. 内联表单 

- 为 `<form>` 元素添加 `.form-inline` 类可使其内容左对齐并且表现为 `inline-block` 级别的控件。只适用于视口（viewport）至少在 768px 宽度时（视口宽度再小的话就会使表单折叠）。

- .sr-only样式将其隐藏

  ```html
  <!--内联表单-->
  <form class="form-inline">
  	<div class="form-group">
  		<label for="username">用户名</label>
  		<input type="text" class="form-control" name="username" id="username" placeholder="请输入用户名" />
  	</div>
  	<div class="form-group">
  		<label for="password">密码</label>
  		<input type="password" class="form-control" name="password" id="password" placeholder="请输入密码" />
  	</div>
  	<div class="form-group">
  		<label for="password">密码</label>
  		<input type="password" class="form-control" name="password" id="password" placeholder="请输入密码" />
  	</div>
  </form>
  ```

### 4.7.2.表单的输入框组、尺寸

	<!--输入框组、尺寸-->
	<form class="form-horizontal">
		<div class="form-group">
			<label for="username">用户名</label>
			<input type="text" class="form-control" name="username" id="username" placeholder="请输入用户名" />
		</div>
		<div class="form-group">
			<label for="password">密码</label>
			<input type="password" class="form-control" name="password" id="password" placeholder="请输入密码" />
		</div>
		<div class="form-group">
			<label for="momey">资产</label>
			<div class="input-group">
				<label class="input-group-addon">@</label>
				<input type="number" class="form-control" name="momey" id="momey" placeholder="请输入你有几块钱" />
				<label class="input-group-addon">@</label>
			</div>
		</div>
		<!--把单选和复选加入到输入组中-->
		<div class="form-group">
			<label for="momey">资产02</label>
			<div class="input-group">
				<label class="input-group-addon">
					<input type="radio"/>
				</label>
				<input type="number" class="form-control" name="momey" id="momey" placeholder="请输入你有几块钱" />
			</div>
		</div>
	</form>
### 4.7.3. 水平排列的表单 

- 通过为表单添加 `.form-horizontal` 类,无需再额外添加 `.row` 了	

```html
<!--水平排列的表单-->
<form class="form-horizontal">
	<div class="form-group">
		<label for="username" class="col-md-1 text-right">用户名</label>
		<div class="col-md-4 ">
			<input type="text" class="form-control" name="username" id="username" placeholder="请输入用户名" />
		</div>
	</div>
	<div class="form-group text-right">
		<label for="password" class="col-md-1">密码</label>
		<div class="col-md-4">
			<input type="password" class="form-control" name="password" id="password" placeholder="请输入密码" />
		</div>
	</div>
</form>
```

### 4.7.4. 被支持的控件 

- 包括大部分表单控件、文本输入域控件，还支持所有 HTML5 类型的输入控件： `text`、`password`、`datetime`、`datetime-local`、`date`、`month`、`time`、`week`、`number`、`email`、`url`、`search`、`tel` 和 `color`。


- 输入框

  ```html
  <input type="text" class="form-control" placeholder="Text input">
  ```

- 文本域

  ```html
  <textarea class="form-control" rows="3"></textarea>
  ```

- 多选和单选框

  - `.disabled` , `.radio`, `.radio-inline`, `.checkbox`, or `.checkbox-inline`都添加在父类中
  - 通过将 `.checkbox-inline` 或 `.radio-inline` 类应用到一系列的多选框（checkbox）或单选框（radio）控件上，可以使这些控件排列在一行。

- 下拉列表（select）

  ```html
  <!--支持的控件-->
  <form>
  	<div class="form-group">
  		<label for="username">用户名</label>
  		<input type="text" class="form-control" name="username" id="username" placeholder="请输入用户名" />
  	</div>
  	<div class="form-group">
  		<label for="password">密码</label>
  		<input type="password" class="form-control" name="password" id="password" placeholder="请输入密码" />
  	</div>
  	<div class="form-group">
  		<label for="info">个人简介</label>
  		<textarea id="info" name="info" class="form-control" rows="5"></textarea>
  	</div>

  	<div class="form-group">
  		<label>性别：</label>
  		<input type="radio" name="gender" value="0" />女
  		<input type="radio" name="gender" value="1" />男

  	</div>

  	<div class="form-group">
  		<label>爱好：</label>
  		<input type="checkbox" name="hobby" value="qdm" />敲代码
  		<input type="checkbox" name="hobby" value="dyx" />打游戏
  	</div>

  	<div class="form-group">
  		<label for="animal">生肖</label>
  		<select name="age" id="age" class="form-control">
  			<option value="horse">马</option>
  			<option value="dog">狗</option>
  			<option value="pig" selected="">猪</option>
  			<option value="mouse">鼠</option>
  		</select>
  	</div>
  </form>
  ```

### 4.7.5. 静态控件 

- `label` 元素放置于同一行，为 `<p>` 元素添加 `.form-control-static` 类即可	

### 4.7.6. 焦点状态 

- 将某些表单控件的默认 `outline` 样式移除，然后对 `:focus` 状态赋予 `box-shadow` 属性

### 4.7.7. 禁用状态 

- 为输入框设置 `disabled` 属性可以禁止其与用户有任何交互（焦点、输入等）。被禁用的输入框颜色更浅，并且还添加了 `not-allowed`鼠标状态。

### 4.7.8. 被禁用的 fieldset 

- 为`<fieldset>` 设置 `disabled` 属性,可以禁用 `<fieldset>` 中包含的所有控件。

  ```html
   <!-- fieldset-disabled -->
  <form>
    <fieldset disabled>
      <div class="form-group">
        <label for="disabledTextInput">姓名</label>
        <input type="text" id="disabledTextInput" class="form-control" placeholder="请输入姓名">
      </div>
      <div class="form-group">
        <label for="disabledSelect">籍贯</label>
        <select id="disabledSelect" class="form-control">
          <option>江苏</option>
        </select>
      </div>
      <div class="checkbox">
        <label>
          <input type="checkbox"> 记住我
        </label>
      </div>
      <button type="submit" class="btn btn-primary">登录</button>
    </fieldset>
  </form>
  <hr>
  ```

### 4.7.9. 只读状态 

- 为输入框设置 `readonly` 属性可以禁止用户修改输入框中的内容,仍然保留标准的鼠标状态。

```html
 <!-- 只读 -->
<form>
  <div class="form-group disabled">
    <label for="email2">电子邮件</label>
    <input type="email" id="email2" class="form-control " placeholder=" 请输入电子邮件 " disabled>
  </div>
  <div class="form-group ">
    <label for="pwd2 ">密码</label>
    <input type="password " id="pwd2 " class="form-control " placeholder="请输入密码" readonly>
  </div>
</form>
<hr/>
```

### 4.7.10. 校验状态 

- 添加 `.has-warning`、`.has-error`或 `.has-success` 类到这些控件的父元素即可

  ```html
  <!-- 校验状态 -->
  <form>
    <div class="form-group has-success">
      <label for="email3">电子邮件</label>
      <input type="email" id="email3" class="form-control" placeholder="请输入电子邮件">
    </div>
    <div class="form-group has-warning">
      <label for="pwd3">密码</label>
      <input type="password" id="pwd3" class="form-control" placeholder="请输入密码">
    </div>
    <div class="form-group has-error">
      <label for="birth">出生地</label>
      <select name="birth" id="birth" class="form-control">
        <option value="江苏">江苏</option>
        <option value="江苏">安徽</option>
      </select>
    </div>
  </form>
  ```

- 添加额外图标

  ```html
   <!-- 添加额外的图标 -->
  <form>
    <div class="form-group has-success has-feedback">
      <label for="email3">电子邮件</label>
      <input type="email" id="email3" class="form-control" placeholder="请输入电子邮件">
      <span class="glyphicon glyphicon-ok form-control-feedback"></span>
    </div>
    <div class="form-group has-warning has-feedback">
      <label for="pwd3">密码</label>
      <input type="password" id="pwd3" class="form-control" placeholder="请输入密码">
      <span class="glyphicon glyphicon-remove form-control-feedback"></span>
    </div>
    <div class="form-group has-error has-feedback">
      <label for="birth2">出生地</label>
      <input type="text" id="birth2" class="form-control" placeholder="出生地">
      <span class="glyphicon glyphicon-warning-sign form-control-feedback" aria-hidden="true"></span>
    </div>
  </form>
  ```

### 4.7.11. 控件尺寸 

- 通过 `.input-lg` 类似的类可以为控件设置高度，通过 `.col-lg-*` 类似的类可以为控件设置宽度。


- `.form-group-lg` 或 `.form-group-sm` 类，为 `.form-horizontal` 包裹的 `label` 元素和表单控件快速设置尺寸。

- 列大小 用栅格系统中的列（column）包裹输入框或其任何父元素，都可很容易的为其设置宽度。

  ```html
   <!-- 尺寸 -->
      <form>
          <div class="form-group">
              <label for="email">电子邮件</label>
              <div class="input-group input-group-lg">
                  <div class="input-group-addon">@</div>
                  <input type="email" id="email" class="form-control" placeholder="请输入电子邮件">
              </div>
          </div>
          <div class="form-group">
              <label for="email">电子邮件</label>
              <div class="input-group input-group">
                  <div class="input-group-addon">@</div>
                  <input type="email" id="email" class="form-control" placeholder="请输入电子邮件">
              </div>
          </div>
          <div class="form-group">
              <label for="email">电子邮件</label>
              <div class="input-group input-group-sm">
                  <div class="input-group-addon">@</div>
                  <input type="email" id="email" class="form-control" placeholder="请输入电子邮件">
              </div>
          </div>
      </form>
      <hr>
      <!-- 水平尺寸 -->
      <form class="form-inline">
          <div class="form-group form-group-lg">
              <label for="email">电子邮件</label>
              <input type="email" id="email" class="form-control " placeholder="请输入电子邮件">
          </div>
          <div class="form-group form-group-sm">
              <label for="pwd">密码</label>
              <input type="password" id="pwd" class="form-control" placeholder="请输入密码">
          </div>
      </form>
      <hr/>
      <!-- 更改列宽 -->
      <form>
          <div class="row">
              <div class="col-xs-2">
                  <label>用户名</label>
                  <input type="text" class="form-control">
              </div>
              <div class="col-xs-3">
                  <label>年龄</label>
                  <input type="text" class="form-control">
              </div>
              <div class="col-xs-4">
                  <label>地址</label>
                  <input type="text" class="form-control">
              </div>
          </div>
      </form>
  ```

- 综合代码 

  ```html
  <!DOCTYPE html>
  <html lang="zh-CN">

  <head>
      <meta charset="utf-8">
      <meta name="viewport" content="width=device-width, initial-scale=1">
      <title>表单</title>
      <link href="css/bootstrap.min.css" rel="stylesheet">
      <script src="js/jquery-1.10.1.min.js"></script>
      <script src="js/bootstrap.min.js"></script>
      <style>
      hr {
          border: 1px solid #666;
      }
      </style>
  </head>

  <body style="margin:30px">
      <!-- 表单基本实例 -->
      <form>
          <div class="form-group">
              <label for="email">电子邮件</label>
              <input type="email" id="email" class="form-control" placeholder="请输入电子邮件">
          </div>
          <div class="form-group">
              <label for="pwd">密码</label>
              <input type="password" id="pwd" class="form-control" placeholder="请输入密码">
          </div>
      </form>
      <hr>
      <!-- 内联表单 -->
      <form class="form-inline">
          <div class="form-group">
              <label for="email" class="sr-only">电子邮件</label>
              <input type="email" id="email" class="form-control" placeholder="请输入电子邮件">
          </div>
          <div class="form-group">
              <label for="pwd">密码</label>
              <input type="password" id="pwd" class="form-control" placeholder="请输入密码">
          </div>
      </form>
      <hr/>
      <!-- 水平排列的表单 -->
      <form class="form-horizontal">
          <div class="form-group">
              <label for="email" class="col-sm-2 control-label">电子邮件</label>
              <div class="col-sm-10">
                  <input type="email" id="email" class="form-control " placeholder="请输入电子邮件">
              </div>
          </div>
          <div class="form-group">
              <label for="pwd" class="col-sm-2 control-label">密码</label>
              <div class="col-sm-10">
                  <input type="password" id="pwd" class="form-control col-sm-8" placeholder="请输入密码">
              </div>
          </div>
      </form>
      <!-- 水平排列的表单 -->
      <form class="form-horizontal">
          <div class="form-group">
              <label for="money" class="col-sm-2  control-label">金额</label>
              <div class="input-group col-sm-6">
                  <div class="input-group-addon">$</div>
                  <input type="text" id="money" class="form-control" placeholder="请输入金额">
                  <div class="input-group-addon">.00</div>
              </div>
          </div>
          <div class="form-group">
              <label for="email" class="col-sm-2  control-label">电子邮件</label>
              <div class="input-group col-sm-6">
                  <div class="input-group-addon">@</div>
                  <input type="email" id="email" class="form-control" placeholder="请输入电子邮件">
              </div>
          </div>
      </form>
      <hr/>
      <!-- 被支持的控件 -->
      <form>
          <!-- 输入框 -->
          <div class="form-group">
              <label for="uname">用户名</label>
              <input id="uname" type="text" class="form-control" placeholder="Text input">
          </div>
          <!-- 文本域 -->
          <div class="form-group">
              <label for="info">个人信息</label>
              <textarea id="info" rows="10" class="form-control">
                  服务协议
              </textarea>
          </div>
          <div class="radio">
              <label>
                  <input type="radio" name="sex" checked>男
              </label>
          </div>
          <div class="radio">
              <label>
                  <input type="radio" name="sex">女
              </label>
          </div>
          <div class="radio disabled">
              <label>
                  <input type="radio" name="sex" disabled>其它
              </label>
          </div>
          <div class="checkbox-inline">
              <label>
                  <input type="checkbox" name="hobby" checked>旅游
              </label>
          </div>
          <div class="checkbox-inline">
              <label>
                  <input type="checkbox" name="hobby">音乐
              </label>
          </div>
          <div class="checkbox-inline">
              <label>
                  <input type="checkbox" name="hobby" checked>读书
              </label>
          </div>
          <div class="checkbox-inline disabled">
              <label>
                  <input type="checkbox" name="hobby" disabled>游泳
              </label>
          </div>
          <select class="form-control">
              <option value="">大专</option>
              <option value="">本科</option>
              <option value="">研究生</option>
          </select>
          <select multiple="" class="form-control">
              <option value="">大专</option>
              <option value="">本科</option>
              <option value="">研究生</option>
          </select>
      </form>
      <hr/>
      <!-- 静态内容 -->
      <form class="form-horizontal">
          <div class="form-group">
              <label class="col-sm-2 control-label">邮箱</label>
              <div class="col-sm-10">
                  <p class="form-control-static">89115008@qq.com</p>
              </div>
          </div>
      </form>
      <!-- fieldset-disabled -->
      <form>
          <fieldset disabled>
              <div class="form-group">
                  <label for="disabledTextInput">姓名</label>
                  <input type="text" id="disabledTextInput" class="form-control" placeholder="请输入姓名">
              </div>
              <div class="form-group">
                  <label for="disabledSelect">籍贯</label>
                  <select id="disabledSelect" class="form-control">
                      <option>江苏</option>
                  </select>
              </div>
              <div class="checkbox">
                  <label>
                      <input type="checkbox"> 记住我
                  </label>
              </div>
              <button type="submit" class="btn btn-primary">登录</button>
          </fieldset>
      </form>
      <hr>
      <!-- 只读 -->
      <form>
          <div class="form-group disabled">
              <label for="email2">电子邮件</label>
              <input type="email" id="email2" class="form-control " placeholder=" 请输入电子邮件 " disabled>
          </div>
          <div class="form-group ">
              <label for="pwd2 ">密码</label>
              <input type="password " id="pwd2 " class="form-control " placeholder="请输入密码" readonly>
          </div>
      </form>
      <hr/>
      <!-- 校验状态 -->
      <form>
          <div class="form-group has-success">
              <label for="email3">电子邮件</label>
              <input type="email" id="email3" class="form-control" placeholder="请输入电子邮件">
          </div>
          <div class="form-group has-warning">
              <label for="pwd3">密码</label>
              <input type="password" id="pwd3" class="form-control" placeholder="请输入密码">
          </div>
          <div class="form-group has-error">
              <label for="birth">出生地</label>
              <select name="birth" id="birth" class="form-control">
                  <option value="江苏">江苏</option>
                  <option value="江苏">安徽</option>
              </select>
          </div>
      </form>
      <!-- 添加额外的图标 -->
      <form>
          <div class="form-group has-success has-feedback">
              <label for="email3">电子邮件</label>
              <input type="email" id="email3" class="form-control" placeholder="请输入电子邮件">
              <span class="glyphicon glyphicon-ok form-control-feedback"></span>
          </div>
          <div class="form-group has-warning has-feedback">
              <label for="pwd3">密码</label>
              <input type="password" id="pwd3" class="form-control" placeholder="请输入密码">
              <span class="glyphicon glyphicon-remove form-control-feedback"></span>
          </div>
          <div class="form-group has-error has-feedback">
              <label for="birth2">出生地</label>
              <input type="text" id="birth2" class="form-control" placeholder="出生地">
              <span class="glyphicon glyphicon-warning-sign form-control-feedback" aria-hidden="true"></span>
          </div>
      </form>
      <!-- 额外元素 -->
      <form>
          <!-- 输入框组(组件) -->
          <div class="form-group">
              <label for="money">金额</label>
              <div class="input-group">
                  <div class="input-group-addon">$</div>
                  <input type="text" id="money" class="form-control" placeholder="请输入金额">
                  <div class="input-group-addon">.00</div>
              </div>
          </div>
          <div class="form-group">
              <label for="email">电子邮件</label>
              <div class="input-group">
                  <div class="input-group-addon">@</div>
                  <input type="email" id="email" class="form-control" placeholder="请输入电子邮件">
              </div>
          </div>
          <!-- 作为额外元素的多选框和单选框 -->
          <div class="input-group">
              <span class="input-group-addon">
            <input type="checkbox">
          </span>
              <input type="text" class="form-control">
          </div>
          <div class="input-group">
              <span class="input-group-addon">
            <input type="radio">
          </span>
              <input type="text" class="form-control">
          </div>
          <!-- 作为额外元素的按钮 -->
          <div class="input-group">
              <span class="input-group-btn">
            <button class="btn btn-success">GO</button>
          </span>
              <input type="text" class="form-control">
          </div>
          <br>
      </form>
      <!-- 额外元素校验 -->
      <form class="form-horizontal">
          <div class="form-group has-success has-feedback">
              <label for="email" class="control-label col-sm-2">电子邮件</label>
              <div class="input-group  col-sm-6">
                  <div class="input-group-addon">@</div>
                  <input type="email" id="email" class="form-control" placeholder="请输入电子邮件">
                  <span class="glyphicon glyphicon-ok form-control-feedback"></span>
              </div>
          </div>
          <div class="form-group has-error has-feedback">
              <label for="pwd" class="control-label col-sm-2">密码</label>
              <div class="input-group  col-sm-6">
                  <div class="input-group-addon">*</div>
                  <input type="password" id="pwd" class="form-control" placeholder="请输入密码">
                  <span class="glyphicon glyphicon-remove form-control-feedback"></span>
              </div>
          </div>
      </form>
      <!-- 尺寸 -->
      <form>
          <div class="form-group">
              <label for="email">电子邮件</label>
              <div class="input-group input-group-lg">
                  <div class="input-group-addon">@</div>
                  <input type="email" id="email" class="form-control" placeholder="请输入电子邮件">
              </div>
          </div>
          <div class="form-group">
              <label for="email">电子邮件</label>
              <div class="input-group input-group">
                  <div class="input-group-addon">@</div>
                  <input type="email" id="email" class="form-control" placeholder="请输入电子邮件">
              </div>
          </div>
          <div class="form-group">
              <label for="email">电子邮件</label>
              <div class="input-group input-group-sm">
                  <div class="input-group-addon">@</div>
                  <input type="email" id="email" class="form-control" placeholder="请输入电子邮件">
              </div>
          </div>
      </form>
      <hr>
      <!-- 水平尺寸 -->
      <form class="form-inline">
          <div class="form-group form-group-lg">
              <label for="email">电子邮件</label>
              <input type="email" id="email" class="form-control " placeholder="请输入电子邮件">
          </div>
          <div class="form-group form-group-sm">
              <label for="pwd">密码</label>
              <input type="password" id="pwd" class="form-control" placeholder="请输入密码">
          </div>
      </form>
      <hr/>
      <!-- 更改列宽 -->
      <form>
          <div class="row">
              <div class="col-xs-2">
                  <label>用户名</label>
                  <input type="text" class="form-control">
              </div>
              <div class="col-xs-3">
                  <label>年龄</label>
                  <input type="text" class="form-control">
              </div>
              <div class="col-xs-4">
                  <label>地址</label>
                  <input type="text" class="form-control">
              </div>
          </div>
      </form>
  </body>

  </html>
  ```

## 4.8.  按钮 

### 4.8.1. 可作为按钮使用的标签或元素 

- 为 `<a>`、`<button>` 或 `<input>` 元素添加按钮类（button class）

  ```html
   <!-- 可作为按钮使用的标签或元素 -->
      <a href="#" class="btn btn-default" role="button">wanho万和</a>
      <button class="btn btn-default">wanho万和</button>
      <input type="button" value="wanho万和" class="btn btn-default">
      <hr>
  ```

### 4.8.2. 预定义样式 

- `btn-default`,`btn-primary`,`btn-success`,`btn-info`,`btn-warning`,`btn-danger`,`btn-link`

  ```html
  <!-- 预定义样式和尺寸 -->
  <button class="btn btn-default">wanho万和</button>
  <button class="btn btn-primary btn-xs">wanho万和</button>
  <button class="btn btn-success btn-sm">wanho万和</button>
  <button class="btn btn-info btn-lg">wanho万和</button>
  <button class="btn btn-warning">wanho万和</button>
  <button class="btn btn-danger">wanho万和</button>
  <button class="btn btn-link">wanho万和</button>
  <hr>
  ```

### 4.8.3. 尺寸 

- 使用 `.btn-lg`、`.btn-sm` 或 `.btn-xs` 就可以获得不同尺寸的按钮。

- `.btn-block` 类可以将其拉伸至父元素100%的宽度

  ```html
  <button class="btn btn-success btn-block">wanho万和</button>
  <!-- .container>.row>.col-sm-4.col-sm-offset-4 -->
  <div class="container">
    <div class="row">
      <div class="col-sm-4 col-sm-offset-4">
        <button class="btn btn-success btn-block">wanho万和</button>
      </div>
    </div>
  </div>
  <hr>
  ```

### 4.8.4. 激活状态 

- 按钮和链接都添加 `.active` 样式

  ```html
  <button type="button" class="btn btn-primary btn-lg active">wanho</button>
  <button type="button" class="btn btn-default btn-lg active">wanho</button>
  <!-- 链接按钮 -->
  <a href="#" class="btn btn-primary btn-lg active" role="button">wanho</a>
  <a href="#" class="btn btn-default btn-lg active" role="button">wanho</a>
  <hr/>
  ```

### 4.8.5. 禁用状态

- 按钮和链接都添加 `disabled` 属性

  ```html
  <!--禁用状态-->
  <button type="button" class="btn btn-lg btn-primary" disabled>wanho</button>
  <button type="button" class="btn btn-default btn-lg" disabled>wanho</button>
  <a href="#" class="btn btn-primary btn-lg " disabled role="button">wanho</a>
  <a href="#" class="btn btn-default btn-lg " disabled role="button">wanho</a>
  ```

## 4.9. 图片 

### 4.9.1. 响应式图片

- 为图片添加 `.img-responsive` 类可以让图片支持响应式布局
- 居中使用 `.center-block` 类，不要用 `.text-center`

### 4.9.2. 图片形状

- `img-rounded`
- `img-circle`
- `img-thumbnail`

```html
<img src="img/zbz.jpg" height="300px" width="200px" alt="" />
<!--图片响应式，等比例变换-->
<img src="img/zbz.jpg" class="img-responsive" alt="" />
<img src="img/zbz.jpg" class="img-circle" alt="" />
```

## 4.10. 辅助类 

### 4.10.1. 情境文本颜色 

```html
<!--文本颜色-->
<p class="text-muted">万和java97</p>
<p class="text-primary">万和java97</p>
<p class="text-success">万和java97</p>
<p class="text-info">万和java97</p>
<p class="text-warning">万和java97</p>
<p class="text-danger">万和java97</p>
```

### 4.10.2. 情境背景色 

```html
<!--文本背景-->
<p class="bg-primary">...</p>
<p class="bg-success">...</p>
<p class="bg-info">...</p>
<p class="bg-warning">...</p>
<p class="bg-danger">...</p>
```

### 4.10.3. 关闭按钮 

```html
<button class="close">&times;</button>
```

### 4.10.4. 三角符号 

```html
<span class="caret"></span>
```

### 4.10.5. 快速浮动 

```html
<!--快速浮动、清楚浮动-->
<!--clearfix相当于overflow: hidden;-->
<div class="clearfix" style="border: 1px solid red;">
  <div class="pull-left" style="border: 1px solid red; width: 80px;">我在左边</div>

  <div class="pull-right" style="border: 1px solid red; width: 80px;">我在右边</div>
</div>
```

### 4.10.6. 让内容块居中 

- 设置`center-block`

  <!--文字居中-->
  <div class="text-center">xxxx</div>
  <!--内容居中-->
  <div class="center-block text-center" style="border: 1px solid red; width: 80px;">xxxx</div>
### 4.10.7. 清除浮动 

- 设置`.clearfix`

### 4.10.8. 显示或隐藏内容 

- `.show` 和 `.hidden` 类

- `.sr-only`

  ```html
  <div class="show">...</div>
  <div class="hidden">...</div> 
  <!--响应式工具：隐藏和显示-->
  <div class="hidden-sm">小屏不可见</div>
  ```

## 4.11. 响应式工具

### 4.11.1. 可用的类 

通过单独或联合使用以下列出的类，可以针对不同屏幕尺寸隐藏或显示页面内容。

|                 | 超小屏幕手机 (<768px) | 小屏幕平板 (≥768px) | 中等屏幕桌面 (≥992px) | 大屏幕桌面 (≥1200px) |
| --------------- | --------------- | -------------- | --------------- | --------------- |
| `.visible-xs-*` | 可见              | 隐藏             | 隐藏              | 隐藏              |
| `.visible-sm-*` | 隐藏              | 可见             | 隐藏              | 隐藏              |
| `.visible-md-*` | 隐藏              | 隐藏             | 可见              | 隐藏              |
| `.visible-lg-*` | 隐藏              | 隐藏             | 隐藏              | 可见              |
| `.hidden-xs`    | 隐藏              | 可见             | 可见              | 可见              |
| `.hidden-sm`    | 可见              | 隐藏             | 可见              | 可见              |
| `.hidden-md`    | 可见              | 可见             | 隐藏              | 可见              |
| `.hidden-lg`    | 可见              | 可见             | 可见              | 隐藏              |

从 v3.2.0 版本起，形如 `.visible-*-*` 的类针对每种屏幕大小都有了三种变体，每个针对 CSS 中不同的 `display` 属性，列表如下：

| 类组                        | CSS `display`            |
| ------------------------- | ------------------------ |
| `.visible-*-block`        | `display: block;`        |
| `.visible-*-inline`       | `display: inline;`       |
| `.visible-*-inline-block` | `display: inline-block;` |

# 5.  组件

## 5.1. 图标、下拉菜单和按钮组 

### 5.1.1. 图标

- Glyphicon Halflings 的字体图标，一般是收费的，允许 Bootstrap 免费使用。

  ```html
  <span class="glyphicon glyphicon-star"></span>
  <i class="glyphicon glyphicon-user"></i>
  <button class="btn btn-default">
    <span class="glyphicon glyphicon-star"></span>
  </button>
  <button class="btn btn-default btn-lg">
    <span class="glyphicon glyphicon-star"></span>
  </button>
  <button class="btn btn-default btn-sm">
    <span class="glyphicon glyphicon-star"></span>
  </button>
  <button class="btn btn-default">
    <span class="glyphicon glyphicon-align-left"></span>
  </button>
  <button class="btn btn-default">
    <span class="glyphicon glyphicon-align-justify"></span>
  </button>
  <button class="btn btn-default">
    <span class="glyphicon glyphicon-align-left"></span>
  </button>
  <button class="btn btn-default">
    <span class="glyphicon glyphicon-align-justify"></span>
  </button>
  <hr/>
  ```

### 5.1.2. 下拉菜单

- 向下包裹在 `.dropdown` 里

  ```html
  <!-- 下拉菜单 -->
      <div class="dropdown">
          <button class="btn btn-default" data-toggle="dropdown">
              下拉菜单<span class="caret"></span>
          </button>
          <ul class="dropdown-menu">
              <li>
                  <a href="#">首页</a>
              </li>
              <li>
                  <a href="#">资讯</a>
              </li>
              <li>
                  <a href="#">课程</a>
              </li>
              <li>
                  <a href="#">万和</a>
              </li>
          </ul>
      </div>
  ```

- 向上包裹在 `.dropup` 里

- 设置对齐方式

  ```html
  <!-- 
  向上触发
  设置菜单项右对齐，默认左对齐
  -->
  <div class="dropup">
    <button class="btn btn-default" data-toggle="dropdown">
      下拉菜单 <span class="caret"></span>
    </button>
    <ul class="dropdown-menu dropdown-menu-right">
      <li>
        <a href="#">首页</a>
      </li>
      <li>
        <a href="#">资讯</a>
      </li>
      <li>
        <a href="#">课程</a>
      </li>
      <li>
        <a href="#">万和</a>
      </li>
    </ul>
  </div>
  ```

- 设置分隔 ` <li class="divider"></li>`

  ```html
   <!-- 
          设置标题
          设置分割线
          设置禁用项
       -->
      <div class="dropdown">
          <button class="btn btn-default" data-toggle="dropdown">
              下拉菜单<span class="caret"></span>
          </button>
          <ul class="dropdown-menu">
              <li class="dropdown-header">万和导航</li>
              <li class="divider"></li>
              <li>
                  <a href="#">首页</a>
              </li>
              <li>
                  <a href="#">资讯</a>
              </li>
              <li>
                  <a href="#">课程</a>
              </li>
              <li>
                  <a href="#">万和</a>
              </li>
              <li class="divider"></li>
              <li class="disabled">
                  <a href="#">关于</a>
              </li>
          </ul>
      </div>
      <hr>
  ```

### 5.1.3. 按钮组

- 按钮组，按钮工具栏

  ```html
  <!-- 按钮组、按钮工具栏 -->
  <div class="btn-toolbar">
    <div class="btn-group">
      <button class="btn btn-default">左</button>
      <button class="btn btn-default">中</button>
      <button class="btn btn-default">右</button>
    </div>
    <div class="btn-group btn-group-sm">
      <button class="btn btn-default">上</button>
      <button class="btn btn-default">中</button>
      <button class="btn btn-default">下</button>
    </div>
  </div>
  ```

- 按钮组中嵌套下拉菜单

  ```html
  <!-- 按钮组中嵌套下拉菜单 -->
      <div class="btn-group">
          <button class="btn btn-default">左</button>
          <button class="btn btn-default">中</button>
          <button class="btn btn-default">右</button>
          <div class="btn-group">
              <button class="btn btn-default dropdown-toggle" data-toggle="dropdown">
                  下拉菜单<span class="caret"></span>
              </button>
              <ul class="dropdown-menu">
                  <li class="dropdown-header">万和导航</li>
                  <li class="divider"></li>
                  <li>
                      <a href="#">首页</a>
                  </li>
                  <li>
                      <a href="#">资讯</a>
                  </li>
                  <li>
                      <a href="#">课程</a>
                  </li>
                  <li>
                      <a href="#">万和</a>
                  </li>
                  <li class="divider"></li>
                  <li class="disabled">
                      <a href="#">关于</a>
                  </li>
              </ul>
          </div>
      </div>
      <br>
  ```

- 垂直菜单 

  ```html
  <!-- 垂直排列 -->
      <div class="btn-group-vertical">
          <button class="btn btn-default">左</button>
          <button class="btn btn-default">中</button>
          <button class="btn btn-default">右</button>
      </div>
  ```

- 两端对齐

  ```html
  <!-- 两端对齐排列的按钮组，使用<a> -->
      <div class="btn-group-justified">
          <a class="btn btn-default">左</a>
          <a class="btn btn-default">中</a>
          <a class="btn btn-default">右</a>
      </div>
      <!-- 如果使用<button>，则需要对每个按钮进行嵌套按钮组 -->
      <div class="btn-group-justified">
          <div class="btn-group">
              <button class="btn btn-default">左</button>
          </div>
          <div class="btn-group">
              <button class="btn btn-default">中</button>
          </div>
          <div class="btn-group">
              <button class="btn btn-default">右</button>
          </div>
      </div>
  ```

## 5.2. 按钮式下拉菜单

### 5.2.1. 单按钮下拉菜单

```html
<!-- 按钮式下拉菜单 -->
<div class="btn-group dropdown">
  <button class="btn btn-default dropdown-toggle" data-toggle="dropdown">
    下拉菜单
    <span class="caret"></span>
  </button>
  <ul class="dropdown-menu">
    <li><a href="#">首页 </a></li>
    <li><a href="#">资讯</a></li>
    <li><a href="#">课程</a></li>
    <li><a href="#">万和</a></li>
  </ul>
</div>
```

### 5.2.2. 分裂式按钮下拉菜单

```html
<!-- 分裂式按钮下拉菜单 -->
<div class="btn-group">
  <button class="btn btn-default">下拉菜单</button>
  <button class="btn btn-default dropdown-toggle" data-toggle="dropdown">
    <span class="caret"></span>
  </button>
  <ul class="dropdown-menu">
    <li><a href="#">首页</a></li>
    <li><a href="#">资讯</a></li>
    <li><a href="#">课程</a></li>
    <li><a href="#">万和</a></li>
  </ul>
</div>
```

### 5.2.3. 尺寸

```html
<!-- 分裂式按钮下拉菜单 -->
<div class="btn-group">
  <button class="btn btn-default btn-lg">下拉菜单</button>
  <button class="btn btn-default dropdown-toggle" data-toggle="dropdown">
    <span class="caret"></span>
  </button>
  <ul class="dropdown-menu">
    <li><a href="#">首页</a></li>
    <li><a href="#">资讯</a></li>
    <li><a href="#">课程</a></li>
    <li><a href="#">万和</a></li>
  </ul>
</div>
```

### 5.2.4. 向上弹出式菜单

```html
<!-- 按钮式下拉菜单 -->
<div class="btn-group dropup">
  <button class="btn btn-default dropdown-toggle btn-lg" data-toggle="dropdown">
    下拉菜单
    <span class="caret"></span>
  </button>
  <ul class="dropdown-menu">
    <li><a href="#">首页 </a></li>
    <li><a href="#">资讯</a></li>
    <li><a href="#">课程</a></li>
    <li><a href="#">万和</a></li>
  </ul>
</div>
```

## 5.3. 输入框、导航、导航条 

### 5.3.1 输入框 

- 基本实例

  ```html
  <div class="input-group">
    <!-- <span class="input-group-addon">@</span> -->
    <input type="text" class="form-control">
    <span class="input-group-addon">@sina.com</span>
  </div>
  ```

- 尺寸

  ```html
  <div class="input-group-lg">
    <!-- <span class="input-group-addon">@</span> -->
    <input type="text" class="form-control">
    <span class="input-group-addon">@sina.com</span>
  </div>
  ```

- 作为额外元素的多选框和单选框

  ```html
  <div class="input-group">
    <span class="input-group-addon">
      <input type="checkbox" name="" id="">
    </span>
    <input type="text" class="form-control">
    <span class="input-group-addon">
      <input type="radio" name="" id="">
    </span>
  </div>
  ```

- 作为额外元素的按钮式下拉菜单

  ```html
  <!-- 使用按钮 -->
  <div class="input-group">
  <input type="text" class="form-control">
  <span class="input-group-btn">
  <button class="btn btn-default">提交</button>
  </span>
  </div>
  <!-- 作为额外元素的按钮式下拉菜单 -->
  <div class="input-group">
    <input type="text" class="form-control">
    <span class="input-group-btn">
      <button class="btn btn-default dropdown-toggle" data-toggle="dropdown">
        下拉菜单
        <span class="caret"></span>
      </button>
      <ul class="dropdown-menu">
        <li><a href="#">首页</a></li>
        <li><a href="#">资讯</a></li>
        <li><a href="#">课程</a></li>
        <li><a href="#">万和</a></li>
      </ul>
    </span>
  </div>
  ```

- 作为额外元素的分裂式按钮下拉菜单

  ```html
  <div class="input-group">
    <input type="text" class="form-control">
    <span class="input-group-btn">
      <button class="btn btn-default">下拉菜单</button>
      <button class="btn btn-default dropdown-toggle" data-toggle="dropdown">
        <span class="caret"></span>
      </button>
      <ul class="dropdown-menu">
        <li><a href="#">首页</a></li>
        <li><a href="#">资讯</a></li>
        <li><a href="#">课程</a></li>
        <li><a href="#">万和</a></li>
      </ul>
    </span>
  </div>
  ```

- 多个按钮

  ```html
  <!-- 多个按钮 -->
  <div class="input-group">
    <input type="text" class="form-control">
    <div class="input-group-btn">
      <button class="btn btn-default">A</button>
      <button class="btn btn-primary">B</button>
    </div>
  </div>
  ```

### 5.3.2 导航 

- 基本导航

  ```html
   <!-- 基本的导航组件 -->
      <ul class="nav nav-tabs">
          <li class="active"><a href="#">首页</a></li>
          <li><a href="#">资讯</a></li>
          <li><a href="#">课程</a></li>
          <li><a href="#">万和</a></li>
      </ul>
      <br>
  ```

- 胶囊式导航

  ```html
  <!-- 胶囊式标签页 -->
  <ul class="nav nav-pills">
  <li class="active"><a href="#">首页</a></li>
  <li><a href="#">资讯</a></li>
  <li><a href="#">课程</a></li>
  <li ><a href="#">万和</a></li>
  </ul>
  ```

- 两端对齐的导航

  ```html
  <ul class="nav nav-pills nav-justified">
  <li class="active"><a href="#">首页</a></li>
  <li><a href="#">资讯</a></li>
  <li><a href="#">课程</a></li>
  <li><a href="#">万和</a></li>
  </ul>
  ```

- 禁用的链接

  ```html
  <ul class="nav nav-pills nav-justified">
    <li class="active"><a href="#">首页</a></li>
    <li><a href="#">资讯</a></li>
    <li><a href="#">课程</a></li>
    <li class="disabled"><a href="#">万和</a></li>
  </ul>
  ```

- 带下拉菜单的导航 

  ```html
   <!-- 带下拉菜单的导航 -->
   <ul class="nav nav-tabs">
   <li class="active"><a href="#">首页</a></li>
   <li><a href="#">资讯</a></li>
   <li><a href="#">课程</a></li>
   <li class="dropdown">
   <a href="#" data-toggle="dropdown">
   万和<span class="caret"></span>
   </a>
   <ul class="dropdown-menu">
   <li><a href="#">li1</a></li>
   <li><a href="#">li2</a></li>
   <li><a href="#">li3</a></li>
   <li><a href="#">li4</a></li>
   </ul>
   </li>
   </ul>
  ```

### 5.3.3 导航条 

- 默认样式的导航条

  ```html
  <nav class="navbar navbar-default">
    <div class="container">

    </div>
  </nav>
  ```

- 品牌图标

  - 设置 `.navbar-brand` 

  ```html
  <!-- 品牌图标 -->
  <nav class="navbar navbar-default">
    <div class="container">
      <div class="navbar-header">
     		<a class="navbar-brand" href="#">brand</a>
      </div>
    </div>
  </nav>
  ```

- 表单

  - 放置于 `.navbar-form` 

  ```html
  <!-- 表单 -->
  <nav class="navbar navbar-default">
    <div class="container">
      <div class="navbar-header">
        <a class="navbar-brand" href="#">brand</a>
      </div>
      <form class="navbar-form" role="search">
        <div class="form-group">
          <div class="input-group">
            <input type="text" class="form-control">
            <span class="input-group-btn">
              <button class="btn btn-default">提交</button>
            </span>
          </div>
        </div>
      </form>
    </div>
  </nav>
  ```

- 按钮

  - `.navbar-btn` 可以被用

- 文本

  - .navbar-text使用

  ```html
   <div class="navbar navbar-default  navbar-static-top navbar-inverse">
     <div class="container">
       <div class="navbar-header">
         <a href="#" class="navbar-brand">
           标题LOGO
         </a>
       </div>
       <ul class="nav navbar-nav">
         <li class="active"><a href="#">首页</a></li>
         <li><a href="#">资讯</a></li>
         <li><a href="#">课程</a></li>
         <li><a href="#">万和</a></li>
       </ul>
       <form class="navbar-form navbar-right">
         <div class="input-group">
           <input type="text" class="form-control">
           <span class="input-group-btn">
             <button class="btn btn-default">搜索</button>
           </span>
         </div>
       </form>
       <button class="btn btn-default navbar-btn navbar-right">跳转</button>
       <p class="navbar-text">
         welcome to <a href="#" class="navbar-link">wanho</a>
       </p>
     </div>
  </div>
  ```

- 组件排列

  - 通过`.navbar-left` 和 `.navbar-right` 工具类让导航链接、表单、按钮或文本对齐。

- 固定在顶部

  - 添加 `.navbar-fixed-top` 

  ```html
  <nav class="navbar navbar-default navbar-fixed-top">
    <div class="container">
      ...
    </div>
  </nav>
  ```

- 固定在底部

  - 添加 `.navbar-fixed-bottom` 类

  ```html
  <nav class="navbar navbar-default navbar-fixed-bottom">
    <div class="container">
      ...
    </div>
  </nav>
  ```

- 静止在顶部

  - 添加 `.navbar-static-top` 类,它会随着页面向下滚动而消失。

  ```html
  <nav class="navbar navbar-default navbar-static-top">
    <div class="container">
      ...
    </div>
  </nav>
  ```

- 反色的导航条

  - 添加 `.navbar-inverse` 类

  ```html
  <nav class="navbar navbar-inverse">
    ...
  </nav>
  ```

## 5.4. 路径导航、分页、标签、微章 

### 5.4.1. 路径导航（面包屑导航）

- `breadcrumb`

```html
<!-- 路径导航，面包屑导航 -->
<ul class="breadcrumb">
  <li><a href="#">首页</a></li>
  <li><a href="#">新闻</a></li>
  <li><a href="#">体育</a></li>
  <li class="active">军事</li>
</ul>
```

### 5.4.2. 分页

- `Page navigation`
- `pagination`
- 不能点击的链接添加 `.disabled` 类、给当前页添加 `.active` 类。

```html
<!-- 分页 -->
<ul class="pagination pagination-lg">
  <li class="disabled"><a href="#">&laquo;</a></li>
  <li class="active"><a href="#">1</a></li>
  <li><a href="#">2</a></li>
  <li><a href="#">3</a></li>
  <li><a href="#">4</a></li>
  <li ><a href="#">5</a></li>
  <li><a href="#">&raquo;</a></li>
</ul>
```

- 建议将 active 或 disabled 状态的链接（即 `<a>` 标签）替换为 `<span>` 标签
- 尺寸：`.pagination-lg` 或 `.pagination-sm`

```html
<!-- 建议将 active 或 disabled 状态的链接（即 <a> 标签）替换为 <span> 标签 -->
<ul class="pagination pagination-lg">
  <li class="disabled"><span href="#">&laquo;</span></li>
  <li class="active"><span href="#">1</span></li>
  <li><a href="#">2</a></li>
  <li><a href="#">3</a></li>
  <li><a href="#">4</a></li>
  <li><a href="#">5</a></li>
  <li><a href="#">&raquo;</a></li>
</ul>
```

- 翻页`pager`

```html
<!-- 翻页 -->
<ul class="pager">
  <li><a href="#">Previous</a></li>
  <li><a href="#">Next</a></li>
</ul>
<!-- 翻页:两端对齐 -->
<ul class="pager">
  <li class="previous disabled"><a href="#">&larr;上一页</a></li>
  <li class="next"><a href="#">下一页&rarr;</a></li>
</ul>
```

### 5.4.3. 标签 

- `label label-*`

```html
<!-- 标签 -->
<h2>万和<span class="label label-default">itany</span></h2>
<h2>万和<span class="label label-success">itany</span></h2>
<h2>万和<span class="label label-danger">itany</span></h2>
<h2>万和<span class="label label-primary">itany</span></h2>
<h2>万和<span class="label label-warning">itany</span></h2>
<h2>万
```

### 5.4.4.  徽章

- 嵌套 `<span class="badge">` 元素

```html
<!-- 徽章 -->
<a href="#">未读消息 <span class="badge">5</span></a>
<br>
<button class="btn btn-primary">
  未读邮件 <span class="badge">15</span>
</button>
<!-- 激活状态自动适配色调 -->
<ul class="nav nav-pills">
  <li><a href="#">首页</a></li>
  <li class="active"><a href="#">消息<span class="badge">5</span></a></li>
</ul>
```

## 5.5. 巨幕、页头、警告框、面板  

### 5.5.1.  巨幕 

- 这是一个轻量、灵活的组件，它能延伸至整个浏览器视口来展示网站上的关键内容。
- `jumbotron`

```html
 <!-- 巨幕 -->
    <div class="container">
        <div class="jumbotron">
            <h1>南京万和</h1>
            <p>南京万和，专业的IT培训机构。。。。</p>
            <p>
                <a href="#" class="btn btn-primary">更多内容</a>
            </p>
        </div>
    </div>
    <hr>
    <!-- 与浏览器等宽，没有圆角 -->
    <div class="jumbotron">
        <div class="container">
            <h1>南京万和</h1>
            <p>南京万和，专业的IT培训机构。。。。</p>
            <p>
                <a href="#" class="btn btn-primary">更多内容</a>
            </p>
        </div>
    </div>
```

### 5.5.2. 页头 

- `h1` 标签内内嵌 `small` 元素

```html
<!-- 页头 -->
<div class="page-header">
  <h1>江苏万和<small>长三角最好的IT教育机构</small></h1>
</div>
```

### 5.5.3. 警告框 

- `.alert` 类是必须要设置的
- 可关闭的警告框
  -  `.alert-dismissible` 类和一个关闭按钮。
- 警告框中的链接
  - 用 `.alert-link` 工具类

```html
<div class="alert alert-success">itany万和</div>
<div class="alert alert-info">itany万和</div>
<div class="alert alert-warning">itany万和</div>
<div class="alert alert-danger">
	<a href="#" class="alert-link">itany万和</a>
	<button class="close" data-dismiss="alert">&times;</button>
</div>
```

### 5.5.4. 面板 

```html
 <!-- 面板 -->
 <div class="panel panel-success">
 <div class="panel-heading">
 <h3 class="panel-title">南京万和</h3>
 </div>
 <div class="panel-body">
 <p>南京万和，专业的IT培训机构。。。。</p>
 </div>
 <div class="panel-footer text-center">
 welcome to wanho
 </div>
 </div>
```

# 6. JavaScript插件

## 6.1. 模态框 

- 静态实例 
- 尺寸：过为 `.modal-dialog`的`modal-lg`或`modal-sm` 增加一个样式调整类实现。
- 禁止动画效果: 删掉 `.fade` 类即可。

```html
<div class="modal fade" tabindex="-1" id="myModal">
  <!-- 窗口声明 -->
  <div class="modal-dialog modal-lg">
    <!-- 内容声明 -->
    <div class="modal-content">
      <!-- 头部、主体、脚注 -->
      <div class="modal-header">
        <button class="close" data-dismiss="modal">&times;</button>
        <h4 class="modal-title">用户登陆</h4>
      </div>
      <div class="modal-body">
        <div class="container-fluid">
          <div class="row">
            <div class="col-xs-6">用户名</div>
            <div class="col-xs-6">请输入用户名</div>
          </div>
          <div class="row">
            <div class="col-xs-6">密码</div>
            <div class="col-xs-6">请输入密码</div>
          </div>
        </div>
      </div>
      <div class="modal-footer">
        <button class="btn btn-primary">登陆</button>
        <button class="btn btn-primary">注册</button>
      </div>
    </div>
  </div>
</div>
```

- 动态实例 

```html
<button class="btn btn-primary btn-lg" data-toggle="modal" data-target="#myModal" data-backdrop="static">弹出模态框</button>
<br>
<a href="#myModal" class="btn btn-success" data-toggle="modal">使用a标签弹出模态框</a>
<br>
<button class="btn btn-info" id="btnOpen">使用JavaScript方式弹出模态框</button>
<script>
  $("#btnOpen").on("click", function() {
    // $("#myModal").modal({
    //    backdrop:true,
    //    keyboard:false,
    //    // show:false,

    // });

    //方法
    $("#myModal").modal('toggle');

    //事件
    $("#myModal").on("show.bs.modal", function() {
      console.log("模态框即将显示出来！");
    });
    $("#myModal").on("shown.bs.modal", function() {
      console.log("模态框已经显示出来！");
    });
    $("#myModal").on("hide.bs.modal", function() {
      console.log("模态框即将隐藏！");
    });
  });
</script>
```

## 6.2.  滚动监听 

- 需要相对定位（relative positioning）
- 通过 data 属性调用
- 事件`activate.bs.scrollspy`:每当一个新条目被激活后都将由滚动监听插件触发此事件。

```html
<body style="margin:50px;">
    <nav class="navbar navbar-default" id="wanho">
        <div class="navbar-header">
            <div class="navbar-brand">南京万和</div>
        </div>
        <ul class="nav navbar-nav">
            <li><a href="#bootstrap">BootStrap</a></li>
            <li><a href="#angularjs">AngularJS</a></li>
            <li><a href="#less">Less</a></li>
            <li class="dropdown">
                <a href="#" data-toggle="dropdown">
                    JavaScript
                    <span class="caret"></span>
                </a>
                <ul class="dropdown-menu">
                    <li><a href="#jquery">jQuery</a></li>
                    <li><a href="#extjs">ExtJS</a></li>
                    <li><a href="#prototype">Prototype</a></li>
                </ul>
            </li>
        </ul>
    </nav>
    <!--  
        data-spy设置监听滚动容器
        data-target设置绑定监听的导航条
        data-offset设置滚动偏移量，默认为10
     -->
    <div id="scroll" data-spy="scroll" data-target="#wanho" data-offset="0" style="height:200px;overflow:auto; padding:0 10px; position:relative;">
        <h4 id="bootstrap">BooStrap</h4>
        <p>
            BooStrap简洁、直观、强悍的前端开发框架，让web开发更迅速、简单。简洁、直观、强悍的前端开发框架，让web开发更迅速、简单。简洁、直观、强悍的前端开发框架，让web开发更迅速、简单。简洁、直观、强悍的前端开发框架，让web开发更迅速、简单。简洁、直观、强悍的前端开发框架，让web开发更迅速、简单。简洁、直观、强悍的前端开发框架，让web开发更迅速、简单。简洁、直观、强悍的前端开发框架，让web开发更迅速、简单。简洁、直观、强悍的前端开发框架，让web开发更迅速、简单。简洁、直观、强悍的前端开发框架，让web开发更迅速、简单。简洁、直观、强悍的前端开发框架，让web开发更迅速、简单。简洁、直观、强悍的前端开发框架，让web开发更迅速、简单。简洁、直观、强悍的前端开发框架，让web开发更迅速、简单。简洁、直观、强悍的前端开发框架，让web开发更迅速、简单。
        </p>
        <h4 id="angularjs">AngularJS</h4>
        <p>
            AngularJS简洁、直观、强悍的前端开发框架，让web开发更迅速、简单。简洁、直观、强悍的前端开发框架，让web开发更迅速、简单。简洁、直观、强悍的前端开发框架，让web开发更迅速、简单。简洁、直观、强悍的前端开发框架，让web开发更迅速、简单。简洁、直观、强悍的前端开发框架，让web开发更迅速、简单。简洁、直观、强悍的前端开发框架，让web开发更迅速、简单。简洁、直观、强悍的前端开发框架，让web开发更迅速、简单。简洁、直观、强悍的前端开发框架，让web开发更迅速、简单。简洁、直观、强悍的前端开发框架，让web开发更迅速、简单。简洁、直观、强悍的前端开发框架，让web开发更迅速、简单。简洁、直观、强悍的前端开发框架，让web开发更迅速、简单。简洁、直观、强悍的前端开发框架，让web开发更迅速、简单。简洁、直观、强悍的前端开发框架，让web开发更迅速、简单。
        </p>
        <h4 id="less">Less</h4>
        <p>
            Less简洁、直观、强悍的前端开发框架，让web开发更迅速、简单。简洁、直观、强悍的前端开发框架，让web开发更迅速、简单。简洁、直观、强悍的前端开发框架，让web开发更迅速、简单。简洁、直观、强悍的前端开发框架，让web开发更迅速、简单。简洁、直观、强悍的前端开发框架，让web开发更迅速、简单。简洁、直观、强悍的前端开发框架，让web开发更迅速、简单。简洁、直观、强悍的前端开发框架，让web开发更迅速、简单。简洁、直观、强悍的前端开发框架，让web开发更迅速、简单。简洁、直观、强悍的前端开发框架，让web开发更迅速、简单。简洁、直观、强悍的前端开发框架，让web开发更迅速、简单。简洁、直观、强悍的前端开发框架，让web开发更迅速、简单。简洁、直观、强悍的前端开发框架，让web开发更迅速、简单。简洁、直观、强悍的前端开发框架，让web开发更迅速、简单。
        </p>
        <h4 id="jquery">jQuery</h4>
        <p>
            jQuery简洁、直观、强悍的前端开发框架，让web开发更迅速、简单。简洁、直观、强悍的前端开发框架，让web开发更迅速、简单。简洁、直观、强悍的前端开发框架，让web开发更迅速、简单。简洁、直观、强悍的前端开发框架，让web开发更迅速、简单。简洁、直观、强悍的前端开发框架，让web开发更迅速、简单。简洁、直观、强悍的前端开发框架，让web开发更迅速、简单。简洁、直观、强悍的前端开发框架，让web开发更迅速、简单。简洁、直观、强悍的前端开发框架，让web开发更迅速、简单。简洁、直观、强悍的前端开发框架，让web开发更迅速、简单。简洁、直观、强悍的前端开发框架，让web开发更迅速、简单。简洁、直观、强悍的前端开发框架，让web开发更迅速、简单。简洁、直观、强悍的前端开发框架，让web开发更迅速、简单。简洁、直观、强悍的前端开发框架，让web开发更迅速、简单。
        </p>
        <h4 id="extjs">ExtJS</h4>
        <p>
            ExtJS简洁、直观、强悍的前端开发框架，让web开发更迅速、简单。简洁、直观、强悍的前端开发框架，让web开发更迅速、简单。简洁、直观、强悍的前端开发框架，让web开发更迅速、简单。简洁、直观、强悍的前端开发框架，让web开发更迅速、简单。简洁、直观、强悍的前端开发框架，让web开发更迅速、简单。简洁、直观、强悍的前端开发框架，让web开发更迅速、简单。简洁、直观、强悍的前端开发框架，让web开发更迅速、简单。简洁、直观、强悍的前端开发框架，让web开发更迅速、简单。简洁、直观、强悍的前端开发框架，让web开发更迅速、简单。简洁、直观、强悍的前端开发框架，让web开发更迅速、简单。简洁、直观、强悍的前端开发框架，让web开发更迅速、简单。简洁、直观、强悍的前端开发框架，让web开发更迅速、简单。简洁、直观、强悍的前端开发框架，让web开发更迅速、简单。
        </p>
        <h4 id="prototype">Prototype</h4>
        <p>
            Prototype简洁、直观、强悍的前端开发框架，让web开发更迅速、简单。简洁、直观、强悍的前端开发框架，让web开发更迅速、简单。简洁、直观、强悍的前端开发框架，让web开发更迅速、简单。简洁、直观、强悍的前端开发框架，让web开发更迅速、简单。简洁、直观、强悍的前端开发框架，让web开发更迅速、简单。简洁、直观、强悍的前端开发框架，让web开发更迅速、简单。简洁、直观、强悍的前端开发框架，让web开发更迅速、简单。简洁、直观、强悍的前端开发框架，让web开发更迅速、简单。简洁、直观、强悍的前端开发框架，让web开发更迅速、简单。简洁、直观、强悍的前端开发框架，让web开发更迅速、简单。简洁、直观、强悍的前端开发框架，让web开发更迅速、简单。简洁、直观、强悍的前端开发框架，让web开发更迅速、简单。简洁、直观、强悍的前端开发框架，让web开发更迅速、简单。
        </p>
    </div>
    <script>
    $('#wanho').on('activate.bs.scrollspy', function() {
        console.log('导航菜单切换。。。');
    });
    </script>
```

## 6.3. 标签页 

```html
<!-- 标签页，也就是选项卡 -->
<!-- <ul class="nav nav-tabs"> -->
<ul class="nav nav-pills">
  <li class="active"><a href="#bootstrap" data-toggle="tab">BootStrap</a></li>
  <li><a href="#html5" data-toggle="tab">HTML5</a></li>
  <li><a href="#css3" data-toggle="tab">CSS3</a></li>
  <li><a href="#angular" data-toggle="tab">Angular</a></li>
</ul>
<div class="tab-content">
  <div class="tab-pane active fade in" id="bootstrap">
    BootStrap.....
  </div>
  <div class="tab-pane" id="html5">
    HTML5.....
  </div>
  <div class="tab-pane" id="css3">
    CSS3.....
  </div>
  <div class="tab-pane" id="angular">
    Angular.....
  </div>
</div>
<script>
  $('.nav a').on('click',function () {
    $(this).tab('show');
  }).on('show.bs.tab',function(){
    console.log('即将显示选项。。。。angular');
  });
</script>
```

## 6.4. 工具提示 

- `tooltip`
- 方向：`data-placement`
- 必须通过js初始化

```html
 <button type="button" class="btn btn-default" data-toggle="tooltip" data-placement="left" title="左边的万和">左边万和</button>
    <button type="button" class="btn btn-default" data-toggle="tooltip" data-placement="top" title="上边的万和">上边万和</button>
    <button type="button" class="btn btn-default" data-toggle="tooltip" data-placement="bottom" title="下边的万和">下边万和</button>
    <button type="button" class="btn btn-default" data-toggle="tooltip" data-placement="right" title="右边的万和">右边万和</button>
    <hr>
    <a href="#" data-toggle="tooltip" title="<strong>welcome to itany</strong>">万和</a>
    <script>
    $('[data-toggle="tooltip"]').tooltip();
    //必须使用JavaScript初始化
    $("a").tooltip({
        animation: false,
        html: true,
        placement: 'right',
        trigger: 'hover',
        // delay:500,
        delay: {
            show: 500,
            hide: 1000,
        },
        template: '<b>wanho</b>',
    });
    </script>
```

## 6.5. 弹出框 和 警告框  

- 4个可能的弹出方向：顶部、右侧、底部和左侧。

```html
<!-- 弹出框 -->
    <button class="btn btn-info" id="btn" data-toggle="popover" title="<strong>wanho</strong>" data-content="<span class='text-info small'>江苏万和是专业的IT培训机构，welcome to wanho...</span>" data-animation="true" data-html="true" data-placement="right" data-trigger="hover" data-delay="500">
        万和
    </button>
    <button class="btn btn-primary" id="btn2">wanho万和</button>
    <br>
    <br>
    <button class="btn btn-default" id="btnShow">显示</button>
    <button class="btn btn-default" id="btnHide">隐藏</button>
    <button class="btn btn-default" id="btnToggle">切换</button>
    <hr>
    <!-- 警告框 -->
    <div class="alert alert-warning">
        <!-- <button class="close" data-dismiss="alert"> -->
        <button class="close" id="btnClose">
            <span>&times;</span>
        </button>
        <p>警告，不允许此操作！</p>
    </div>
    <script>
    $('#btn').popover();

    //使用JavaScript方式
    $('#btn2').popover({
        title: '<strong>welcome to wanho</strong>',
        content: '<span class="text-info small">南京万和是专业的IT培训机构，welcome to wanho...</span>',
        animation: true,
        html: true,
        placement: 'right',
        delay: 0,
    });

    //方法
    $('#btnShow').on('click', function() {
        $('#btn').popover('show');
    });
    $('#btnHide').on('click', function() {
        $('#btn').popover('hide');
    });
    $('#btnToggle').on('click', function() {
        $('#btn').popover('toggle');
    });

    //事件
    $('#btn').on({
        'show.bs.popover': function() {
            console.log('即将显示');
        },
        'hide.bs.popover': function() {
            console.log('即将隐藏');
        }
    });

    //关闭按钮
    $('#btnClose').on('click', function() {
        $(".alert").alert('close');
    })
    </script>
```

## 6.6. 折叠 、面板组、 手风琴 折叠效果 

```html
<!-- 基本实例 -->
<button class="btn btn-primary" data-toggle="collapse" data-target="#content">
  万和
</button>
<div id="content" class="collapse">
  <div class="well">
    万和是专业的IT培训机构。。。。 万和是专业的IT培训机构。。。。 万和是专业的IT培训机构。。。。 万和是专业的IT培训机构。。。。
  </div>
</div>
<button class="btn btn-success" id="btnOpen">打开折叠内容</button>
 <script>
   $('#btnOpen').on('click', function() { $('#content').collapse('toggle'); });
</script>
```

```html
<!-- 手风琴折叠效果 -->
<div class="panel-group" id="wanho">
  <div class="panel panel-default">
    <div class="panel-heading">
      <!-- <a href="#one"class="panel-title"data-toggle="collapse"data-parent="#wanho">第一部分</a> -->
      <a href="#one" class="panel-title">第一部分</a>
    </div>
    <div class="panel-collapse collapse" id="one">
      <div class="panel-body">
        第一部分的内容。。。。。。 第一部分的内容。。。。。。
      </div>
    </div>
  </div>
  <div class="panel panel-default">
    <div class="panel-heading">
      <a href="#two" class="panel-title">第二部分</a>
    </div>
    <div class="panel-collapse collapse" id="two">
      <div class="panel-body">
        第二部分的内容。。。。。。 第二部分的内容。。。。。。
      </div>
    </div>
  </div>
  <div class="panel panel-default">
    <div class="panel-heading">
      <a href="#three" class="panel-title">第三部分</a>
    </div>
    <div class="panel-collapse collapse" id="three">
      <div class="panel-body">
        第三部分的内容。。。。。。 第三部分的内容。。。。。。
      </div>
    </div>
  </div>
</div>
<script>
    $('#wanho .collapse').collapse({ toggle: false, parent: '#wanho', });
    $('#wanho a').on('click', function() { $(this).parent().siblings().collapse('toggle'); })
</script>
```













