# javaScript

[TOC]



## 1.简介

- JavaScript 是属于网络的脚本语言！

- JavaScript 被用来改进设计、验证表单、检测浏览器、创建cookies，以及更多的应用。

- JavaScript 是因特网上最流行的脚本语言，这门语言可用于 HTML 和 web，更可广泛用于服务器、PC、笔记本电脑、平板电脑和智能手机等设备。

  ​

  ​

  JavaScript web 开发人员必须学习的 3 门语言中的一门：

  1. **HTML** 定义了网页的内容
  2. **CSS** 描述了网页的布局
  3. **JavaScript** 网页的行为

  本教程是关于 JavaScript 及介绍 JavaScript 如何与 HTML 和 CSS 一起工作。

## 2.历史发展

- JavaScript 由 Brendan Eich 发明。它于 1995 年出现在 Netscape 中（该浏览器已停止更新），并于 1997 年被 ECMA（一个标准协会）采纳。

- 1997年ECMA(国际化标准组织)会员大会采纳了它的首个版本，将其列入到其规范中。
- JavaScript 的正式名称是ECMAScript，这个标准由 ECMA 组织发展和维护。ECMAScript其实是规范的制定者，而JavaScript 规范的实现者

## 3.JavaScript组成

- BOM (Browser Object Model)	浏览器对象模型
- DOM (Document Object Model) 文档对象模型

## 4.JavaScript的基本结构

- 注释

```
HTML 中的脚本必须位于 <script> 与 </script> 标签之间。

脚本可被放置在 HTML 页面的 <body> 和 <head> 部分中。

<script type="text/javascript">
        //单行
        /*多行*/
</script>
```

- 示例

```
<script type="text/javascript">
	document.write("hello javascript <br/>");
	//system.out.println("hello world")
	document.writeln("hello web")
	document.writeln("hello java")
	document.writeln("<hr/>")
	document.write("hello")
	document.write("rt")
</script>
```

注

- script标签可以放置在任意地方，但使用时考虑加载性能的时机问题，一般放置在head中或body结束标签前，建议放在body结束标签前
- write()与writeln()方法几乎是一样的，差别仅在于后者将在所写的字符串后面加一个换行符。在HTML通常是生成一个空格。

## 5.JavaScript的三种使用范围

- 行内
- 当前页
- 当前站点(每一个页面，需要手动引入)

```
<body>
	<!--行内-->
	<button onclick="document.writeln('java97')">按钮</button>
	<hr/>
	<!--全局-->
	<script type="text/javascript" src="js/main.js"></script>
	<!--当前页-->
	<script type="text/javascript">
		document.write("hello javascript <br/>");
		document.writeln("hello wangqi")
		document.writeln("hello chenwei")
	</script>
</body>
```

## 6.变量

因为JavaScript是弱数据类型，因此在声明时使用的var，真实的数据类型取决于所赋予的值

声明有三种方式



- 变量必须以字母开头
- 变量也能以 $ 和 _ 符号开头（不过我们不推荐这么做）
- 变量名称对大小写敏感（y 和 Y 是不同的变量）

当向变量分配文本值时，应该用双引号或单引号包围这个值。

当向变量赋的值是数值时，不要使用引号。如果您用引号包围数值，该值会被作为文本来处理。



- 先声明再赋值

  ```javascript
  //先声明再赋值
      var i;
      i = 100;
      document.write(i + "<br/>");
  ```

- 声明时同时赋值

  ```javascript
  //声明时同时赋值
      var j = 200;
      document.write(j + "<br/>");
  ```

- 不声明直接使用

  ```javascript
   //不声明直接使用
      k = 300;
      document.write(k + "<br/>");
  ```

- 注

  - 声明的变量作用域:看变量声明的位置，放置在函数中即为局部变量，放置在script标签即为全局变量
  - 未声明直接使用的变量记远是全局变量

  ```javascript
  <script type="text/javascript">
      //全局
      var i = 141;
      //声明函数
      function show() {
          //局部变量
          var num = 100;
          //全局
          k = 369;
      }
      //调用函数
      show();
      // document.write(num + "<br/>"); //访问不到
      document.write(i + "<br/>"); //141
      document.write(k + "<br/>"); //369
   </script>
  ```

## 7.数据类型





JS是一种弱类型语言。JS拥有动态类型，相同的变量可以用作不同的类型。
JS有7种数据类型：三种基本类型（**数字，字符串，布尔**），两种引用数据类型（**对象，数组**)，两种特殊数据类型（**undefined，null**）。JS有5种原始类型：数字，字符串，布尔，undefined，null。



在JavaScript中的数据类型如下：

- undefined     :	没有赋过值的变量，此时变量为undefined类型

- object             :       赋值为null或对象，此时变量为object类型

- number          :       赋值为整数和浮点，此时变量为number类型

- var x1=34.00;
  var x2=34;
  var y=123e5;
  var z=123e-5;
  document.write(x1 + "<br>")
  document.write(x2 + "<br>")
  document.write(y + "<br>")
  document.write(z + "<br>")

- string              :       赋值为'xxx'或"xxx"，此时变量为string类型

  var carname1="Volvo XC60";
  var carname2='Volvo XC60';
  var answer1='It\'s alright';
  var answer2="He is called \"Johnny\"";
  var answer3='He is called "Johnny"';
  document.write(carname1 + "<br>")
  document.write(carname2 + "<br>")
  document.write(answer1 + "<br>")
  document.write(answer2 + "<br>")
  document.write(answer3 + "<br>")

- boolean          :       赋值true和false，此时变量为boolean类型

- null为空对象，只有一个值，null
  null表示尚未存在的对象。
  当函数返回的对象不存在时，返回null。
  当某个对象不需要时，可将值设为null。

```
<script type="text/javascript">
    var i;
    document.write(typeof(i) + "<br/>"); //undefined
    i = null;
    document.write(typeof(i) + "<br/>"); //object
    i = new Date()
    document.write(typeof(i) + "<br/>"); //object
    i = 10;
    document.write(typeof(i) + "<br/>"); //number
    i = 10.5;
    document.write(typeof(i) + "<br/>"); //number
    i = "abc";
    document.write(typeof(i) + "<br/>"); //string
    i = "false";
    document.write(typeof(i) + "<br/>"); //string
    i = false;
    document.write(typeof(i) + "<br/>"); //boolean
</script>
```





## 8.string类型的常用属性和方法

- 属性

  - length属性：表示字符串的长度

- 方法

  - concat()       连接字符串
  - charAt()       返回在指定位置的字符
  - indexOf()     返回某个指定的字符串值在字符串中首次出现的位置
  - lastIndexOf()      从后向前搜索字符串
  - split()        把字符串分割为字符串数组。
  - substr()     可在字符串中抽取从 start 下标开始的指定数目的字符。
  - substring()     提取字符串中两个指定的索引号之间的字符(前包，后不包)
  - slice()        提取字符串的某个部分，并以新的字符串返回被提取的部分（可负数、不建议使用）
  - toString()    返回字符串
  - toUpperCase()      转大写
  - toLowerCase()      转小写
  - match()       找到一个或多个正则表达式的匹配
  - search()       检索与正则表达式相匹配的值
  - replace()     用于在字符串中用一些字符替换另一些字符，或替换一个与正则表达式匹配的子串
  - trim()        去空格

- 正则表达式

  ​

  正则表达式（英语：Regular Expression，在代码中常简写为regex、regexp或RE）使用单个字符串来描述、匹配一系列符合某个句法规则的字符串搜索模式。

  ​

  正则表达式是由一个字符序列形成的搜索模式。

  当你在文本中搜索数据时，你可以用搜索模式来描述你要查询的内容。

  正则表达式可以是一个简单的字符，或一个更复杂的模式。

  正则表达式可用于所有文本搜索和文本替换的操作。

  ## 正则表达式修饰符

  **修饰符** 可以在全局搜索中不区分大小写:

  | 修饰符  | 描述                           |
  | ---- | ---------------------------- |
  | i    | 执行对大小写不敏感的匹配。                |
  | g    | 执行全局匹配（查找所有匹配而非在找到第一个匹配后停止）。 |
  | m    | 执行多行匹配。                      |

  ------

  ## 正则表达式模式

  方括号用于查找某个范围内的字符：

  | 表达式    | 描述               |
  | ------ | ---------------- |
  | [abc]  | 查找方括号之间的任何字符。    |
  | [0-9]  | 查找任何从 0 至 9 的数字。 |
  | (x\|y) | 查找任何以 \| 分隔的选项。  |

  元字符是拥有特殊含义的字符：

  | 元字符    | 描述                            |
  | ------ | ----------------------------- |
  | \d     | 查找数字。                         |
  | \s     | 查找空白字符。                       |
  | \b     | 匹配单词边界。                       |
  | \uxxxx | 查找以十六进制数 xxxx 规定的 Unicode 字符。 |

  量词:

  | 量词   | 描述                    |
  | ---- | --------------------- |
  | n+   | 匹配任何包含至少一个 *n* 的字符串。  |
  | n*   | 匹配任何包含零个或多个 *n* 的字符串。 |
  | n?   | 匹配任何包含零个或一个 *n* 的字符串。 |

  - ```
    /^xxx$/    ^表示开始    $表示结束  联想一下电话号码/^1[34578]\d{9}$/
    ```

- == 与===区别

  - ==等于，===全等（值和类型）
  - == 两值类型不同时候，先进行类型转换，再比较
  - ===不做类型转换，类型不同肯定返回false

```
		 <script type="text/javascript">
    document.write("abc123".length + "<br/>");
    document.write("a" + "b" + "<br/> "); //ab
    document.write("1" + "2" + "<br/> "); //12
    document.write("a" + 1 + 2 + "<br/> "); //a12
    document.write(1 + 2 + "<br/> "); //3
    document.write(1 + 2 + "a" + "<br/> "); //3a
    document.write("a".concat("b") + "<br/> "); //ab
    document.write("abc".charAt(1) + "<br/> "); //b
    document.write("abcabc".indexOf('b') + "<br/> "); //1
    document.write("abcabc".lastIndexOf('b') + "<br/> "); //4
    document.write("abcabc".indexOf('b', 3) + "<br/> "); //4
    document.write("abc123".substring(1, 4) + "<br/> "); //bc1
    document.write("abc123".substring(1) + "<br/> "); //bc123
    document.write("abc123".substr(1, 4) + "<br/> "); //bc12
    document.write("abc123abc".slice(-3, -1) + "<br/> "); //ab
    document.write("a,b,c".split(",") + "<br/> "); //[a,b,c]
    document.write("a.b.c".split(".") + "<br/> "); //[a,b,c]
    document.write("wanHO".toLowerCase() + "<br/> "); //wanho
    document.write("wanHO".toUpperCase() + "<br/> "); //WANHO
    document.write("wanHO".toString() + "<br/> "); //wanHO
    document.write(" 1 2 ".length + "<br/> "); //5
    document.write(" 1 2 ".trim().length + "<br/> "); //3
    
    /*正则表达式*/
    var phoneStr="13913001391";
    var phoneReg=/^1[34578]\d{9}$/;//百度
    document.writeln(typeof(phoneReg)+"<br/>");
    
    var regex = "^((13[0-9])|(14[5|7])|(15([0-3]|[5-9]))|(18[0,5-9]))\\d{8}$";
	s = "13913007563";
	document.write(s.match(regex) + "<br/>");//返回匹配的字符串
	document.write(s.search(regex) + "<br/>");//0
	
	/*找到一个或多个正在表达式的匹配*/
    document.writeln(phoneStr.match("1300")+"<br/>");
    document.writeln(phoneStr.match(phoneReg)+"<br/>");
    console.log(phoneStr.match(phoneReg));
    /*检索与正则表达式相匹配的值。0,-1*/
    document.writeln(phoneStr.search(phoneReg)+"<br/>");
    /*替换，替换第一个值*/
    document.writeln(phoneStr.replace("9","3")+"<br/>");
    document.writeln(phoneStr.replace(/^1[34578]\d{9}$/,"是一个电话号码")+"<br/>");
	
	/*java：==（全等）、equals(相等)*/
	/*===（全等）、==(相等)区别*/
    var b = true;
    document.write((1 == 1) + "<br/> "); //true
    document.write((1 == b) + "<br/> "); //true
    document.write((!undefined) + "<br/> "); //true
    document.write((1 == "1") + "<br/> "); //true
    document.write((1 === "1") + "<br/> "); //false
 </script>
```







## 9.数组

### 9.1. 语法

- 先声明，再初始化

```html
<script type="text/javascript">
  	//int  arr=new int[10];
    //先声明
    var arr;
    //再初始化
    arr = new Array(3); //初始数据长度，注意不是上限
    //打印数组长度
    document.write(arr.length + "<br/>");
    //赋值
    arr[0] = "abc"
    arr[1] = false;
    arr[4] = 100;
    //取值
    document.write(arr[0] + "<br/>");
    document.write(arr[1] + "<br/>");
    //打印数组长度
    document.write(arr.length + "<hr/>");
    //遍历出所有内容 
    for (var i = 0; i < arr.length; i++) {
        document.write(arr[i] + "<br/>");
    }
    // for的加强版，会过滤掉undefined的值，遍历也是下标 
    for (var index in arr) {
        document.write(arr[index] + "<br/>");
    }
 	//JS数组==Java数组、Java集合
</script>
```

- 声明时，同时初始化值（多种声明数方式）

```javascript
var arr = new Array("aa", "bb", "cc");
var arr = ["aa", "bb", "cc"];
var arr = new Array(10);
arr[1] = "aaa";
arr[2] = "bbb";
arr[3] = "ccc";
document.write(arr + "<br/>")
document.write("<hr/>");
var arr01 = new Array("aaa", "bbb", "ccc");
for(var i = 0; i < arr01.length; i++) {
	document.write(arr01[i] + "<br/>");
}
document.write("<hr/>");
var arr02 = ["aaa", "bbb", "ccc"];
for(var i = 0; i < arr02.length; i++) {
	document.write(arr02[i] + "<br/>");
}
document.write(arr02 + "<br/>")
var arr03 = [];
for(var i = 50; i < 100; i++) {
	arr03[i] = "";
}
document.write(typeof(arr03[60]));
document.write(arr03 + "<br/>")
```

### 9.2. 赋值和取值

都是通过下标进行的，下标从0开始

- 赋值

  - 数组名[下标]=值;
- 取值

  - 数组名[下]
- 注
  - 下标的最大值==数组的.length-1;

  - 如果下标超过最大值，JavaScript是不会报错的，只是打印此值为undefined

  - 数组中的元素没有赋值，就是undefined

    ​

### 9.3. 常用属性和方法

- 属性

  - length:表示数组的长度

- 方法

  | [Array](ch23-37-fm2xml.html)             | 对数组的内部支持          |
  | ---------------------------------------- | ----------------- |
  | [Array.concat( )](ch23-47-fm2xml.html)   | 连接数组              |
  | [Array.join( )](ch23-54-fm2xml.html)     | 将数组元素连接起来以构建一个字符串 |
  | [Array.length](ch23-61-fm2xml.html)      | 数组的大小             |
  | [Array.pop( )](ch23-64-fm2xml.html)      | 删除并返回数组的最后一个元素    |
  | [Array.push( )](ch23-70-fm2xml.html)     | 给数组添加元素           |
  | [Array.reverse( )](ch23-77-fm2xml.html)  | 颠倒数组中元素的顺序        |
  | [Array.shift( )](ch23-81-fm2xml.html)    | 将元素移出数组           |
  | [Array.slice( )](ch23-87-fm2xml.html)    | 返回数组的一部分          |
  | [Array.sort( )](ch23-95-fm2xml.html)     | 对数组元素进行排序         |
  | [Array.splice( )](ch23-101-fm2xml.html)  | 插入、删除或替换数组的元素     |
  | [Array.toLocaleString( )](ch23-109-fm2xml.html) | 把数组转换成局部字符串       |
  | [Array.toString( )](ch23-115-fm2xml.html) | 将数组转换成一个字符串       |
  | [Array.unshift( )](ch23-122-fm2xml.html) | 在数组头部插入一个元素       |

- 添加

  - push()向数组的末尾添加一个或更多元素，并返回新的长度。

  - unshift()向数组的开头添加一个或更多元素，并返回新的长度。

  - splice(index,howmany,item1,...,item2)删除元素，并向数组添加新元素。

    | index             | 必需。整数，规定添加/删除项目的位置，使用负数可从数组结尾处规定位置。 |
    | ----------------- | ----------------------------------- |
    | howmany           | 必需。要删除的项目数量。如果设置为 0，则不会删除项目。        |
    | item1, ..., itemX | 可选。向数组添加的新项目。                       |

- 删除

  - splice()删除元素，并向数组添加新元素
  - pop()删除并返回数组的最后一个元素
  - shift()删除并返回数组的第一个元素

- 截取和合并

  - slice()从某个已有的数组返回选定的元素
  - concat()连接两个或更多的数组，并返回结果。

- 排序

  - sort()
  - reverse()颠倒数组中元素的顺序。

- 转字符串

  - toString()
  - toLocaleString()
  - join()

```html
<script type="text/javascript">
	/*数组的属性：length*/
	/*数组的放法*/
	var arr = [];
	/*push:加后面，返回新的长度*/
	arr.push("aaa2");
	arr.push("bbb3");
	arr.push("ccc4");
	/*unshift:加前面*/
	arr.unshift("ddd1");
	arr.unshift("eee0");

	/*删除并返回数组的最后一个元素*/
	document.writeln(arr.pop() + "<hr/>");
	/*删除并返回数组的第一个元素*/
	document.writeln(arr.shift() + "<hr/>");

	for(var i = 0; i < arr.length; i++) {
		document.writeln(arr[i] + "<br/>");
	}
	document.writeln(arr.join("-") + "<hr/>");

	var arr2 = ["123a", "蒋蕾", 1, "aaa", "ccc", "bbb"];

	/*排序*/
	//arr2.sort();
	/*颠倒：不是倒序*/
	//arr2.reverse();

	/*截图:前包后不包，可负数*/
	document.writeln(arr2.slice(-3, -2) + "<hr/>");

	/*splice()：删除元素，并向数组添加新元素。*/
	/*语法：arrayObject.splice(index(下标),howmany(数量),element1,.....,elementX)*/
	/*删除指定位置后面多少个元素*/
	/*添加指定位置后面多少个元素howmany：0 */
	arr2.splice(1, 0, "123b", "123c");
	arr2.splice(4, 0, "gay斌");

	for(var i = 0; i < arr2.length; i++) {
		document.writeln(arr2[i] + "<br/>");
	}
	document.writeln("<hr/>");
	var arr3 = [1, 2, 3];
	var arr4 = ["a", "b", "c"];
	var arr5 = arr3.concat(arr4);
	for(var i = 0; i < arr5.length; i++) {
		document.writeln(arr5[i] + "<br/>");
	}
</script>
```

## 10.运算符

- 算术运算符
  - 一元 ++	--
  - 二元 * / % +- 
- 关系运算符
  - < <= > >=
  - == !=
  - === 严格
- 逻辑运算符 ! && ||
- 赋值运算符
  - =
  - *=    /=     %=      +=            -=

| 运算符  | 例子   | 等价于   | 结果   |
| ---- | ---- | ----- | ---- |
| =    | x=y  |       | x=5  |
| +=   | x+=y | x=x+y | x=15 |
| -=   | x-=y | x=x-y | x=5  |
| *=   | x*=y | x=x*y | x=50 |
| /=   | x/=y | x=x/y | x=2  |
| %=   | x%=y | x=x%y | x=0  |

- 三元运算符
  - 条件?值1:值2

```
<script type="text/javascript">
    //算术运算符
    //在JavaScript整数和浮点都为number类型，所以5/2结果也是number类型，2.5当然是number类型
    document.write(2 / 1 + "<br/>"); //2
    document.write(5 / 2 + "<br/>"); //2.5
    document.write(5 % 2 + "<br/>"); //1
    var i = 10;
    document.write(++i + "<br/>"); //11
    document.write(i++ + ++i + "<br/>"); //11+13 
    // 关系
    document.write((5 >= 2) + "<br/>"); //1
    document.write((false === 0) + "<br/>"); //false
    //逻辑
    document.write((!true) + "<br/>"); //false
    document.write((!1) + "<br/>"); //false
    document.write((!undefined) + "<br/>"); //true
    document.write((true && true) + "<br/>"); //true
    document.write((true || false) + "<br/>"); //true
    var j = 5;
    document.write((false && ++j > 0) + "<br/>"); //false
    document.write(j + "<br/>"); //5
    document.write((true || ++j > 0) + "<br/>"); //true
    document.write(j + "<br/>"); //5
    //赋值
    j %= 10;
    document.write(j + "<br/>"); //5
    //三元
    document.write((5 > 32 ? true : false) + "<br/>"); //false
</script>
```

## 11.流程控制

- 分支结构
  - if
  - switch-case
- 循环结构
  - while
  - do-while
  - for
  - 循环中有两个关键字
    - break	:    结束当前循环
    - continue :  结束本次循环，继续下次循环

```
<script type="text/javascript">
	if(3 > 12) {
		document.write("true" + "<br/>")
	} else {
		document.write("false" + "<br/>")
	}
	var a = 1;
	switch(a) {
		case 1:
			document.write("我是第一名" + "<br/>");
			break;
		case 2:
			document.write("我是第二名" + "<br/>");
			break;
		case 30:
			document.write("我是最后一名" + "<br/>");
			break;
	}
	var i = 1;
	var sum = 0;
	while(i < 11) {
		sum += 1;
		i++;
	}
	document.write(sum + "<br/>");
	//do-while
	do {
		sum += 1;
		i++;
		document.write(sum + "<br/>");
	} while (i < 11)
</script>
```

## 12.注释

- 在HTML中 <!-- -->
- 在CSS中 /* */
- 在JavaScript中
  - 单行: //
  - 多行: /* */

## 13.函数

### 11.1. 内置函数

- alert("内容"): 警告框
- prompt("提示消息","默认值" ) : 输入框
- confirm( ) : 确认框
- Number("") ：转Number类
- parseInt(""):   转Number的整数类型
- parseFloat(" "): 转Number的浮点类型
- isNaN( "xxx"): 是否不是一个数字，数字返回false

```
<script type="text/javascript">
	/*警告！*/
	//alert("警告框！")
	/*输入框*/
	var s1 = window.prompt("请输入一个数字");
	var s2 = prompt("请输入另一个数字");
	document.write(typeof(s1) + "<br/>")
	document.write(isNaN(s1) + "<br/>")
	document.write(s1 + s2 + "<hr/>")
	document.write(parseInt(s1) + parseInt(s2) + "<hr/>")
	document.write(parseFloat(s1) + parseFloat(s2) + "<hr/>");
	document.write(typeof(parseInt(s1)) + "<hr/>")
	document.write(typeof(Number(s1)) + "<hr/>")
	document.write(parseInt(s1) + "<hr/>")
	document.write(Number(s1) + "<hr/>")
	/*确认框*/	
	var b = confirm("国庆真八天假期？");
	document.write(b + "<hr/>")
	if(b) {
		document.write("是真的啦~" + "<hr/>")
	} else {
		document.write("国庆加敲代码！" + "<hr/>")
	}
</script>
```

### 11.2. 自定义函数

语法 ：

​	function 函数名(参数列表){

​		函数值;

​		[return 值;]

​	}

​	注:

- 在声明函数时，不能加var，否则有语法错误 
- 在JavaScript中同有函数重载的概念，函数名一样，后面声明的函数会覆盖前面的函数
- 声明函数时有3个参数，调用时可不传参数，可传多个参数，甚至超过3个参数
- 匿名函数

```
<script type="text/javascript">
	/*自定义函数*/
	function show(k) {
		document.write(k + "<br/>");//100
		k = 10;
		document.write("好好敲代码~~" + k + "<br/>");//10
	}
	show(100);
	function add(i, j, k) {
		document.write(i + j + k + "<br/>");
	}
	add("s", 2, 3);//s23
	add(1, 2, "a");//3a
	add(10, 20);//NaN
	add(10, 20, 30, 40, 50, 60, 250);//60

	/*匿名函数1*/
	var myshow = function() {
		document.write("我是有一个匿名函数。。。" + "<br/>");
	}
	myshow();
	/*匿名函数2*/
	(function() {
		document.write("我是另一个匿名函数。。。" + "<br/>");
	})();
</script>
```

## 14.BOM 浏览器对象模型

结构:(树形图)

### 14.1. 属性对象

#### 14.1.1. history对象

- 方法

  - back( )
  - forward( )
  - go( )
    - go(1)=forward()
    - go(-1)=back()
    - 如果跳转的页面不存，则无效

  ```html
  <h1>星期二</h1>
  <a href="monday.html">星期一</a>
  <a href="tuesday.html">星期二</a>
  <a href="sunday.html">星期日</a>
  <hr/>
  <a href="javascript:window.history.back()">上</a>
  <a href="javascript:window.history.forward()">下</a>
  <a href="javascript:window.history.go(-1)">上</a>
  <a href="javascript:window.history.go(1)">下</a>
  <a href="javascript:window.history.go(2)">下2</a>
  ```

#### 14.1.2. location对象

- 属性
  - href : 设置或返回URL
  - host : 返回当前主机名和当前URL端口号
  - hostname : 返回当前主机名
- 方法
  - reaload() : 重新加载当前面
  - replace() : 替换当前页面

```html
<script type="text/javascript">
	document.writeln(typeof(window)+"<br/>");
	document.writeln(typeof(window.location)+"<br/>");
	document.writeln(typeof(window.location.host)+"<br/>");
	document.writeln(window.location.href+"<br/>");
	document.writeln(window.location.host+"<br/>");
	document.writeln(window.location.hostname+"<br/>");
	document.writeln(window.location.port+"<br/>");
	document.writeln(window.location.search+"<br/>");
	
	function show1(){
		/*window可以省略*/
		/*reload():刷新*/
		location.reload()
	}
	function show2(){
		/*replace():替换当前文档,无法回退*/
		location.replace("https://www.baidu.com/");
	}
	function show3(){
		/*assign():加载新的文档，可回退*/
		location.assign("https://www.baidu.com/");
		
	}
	
	function show4(){
		/*用的最多的*/
		location.href="https://www.baidu.com/";
		
	}
</script>
</head>
<body>
  <input type="text" />
  <button onclick="show1()">刷新</button>
  <button onclick="show2()">百度2</button>
  <button onclick="show3()">百度3</button>
  <button onclick="show4()">百度4</button>
</body>
```

### 14.2. window的常用方法

- alert( )		警告框
- prompt( )        输入框
- confirm( )        确认
- open( )           打开窗体
  - width
  - height
  - left
  - top
  - toolbar
  - scrollbars
  - location
  - status
  - menubar
  - resizable
  - titlebar
  - fullscreen
- close( )           关闭窗体
- setTimeout( )   :在指定的毫秒后调用一次函数，只调用一回 
- setInterval( )   : 在间隔的毫秒后调用函数，一直调用一回 
- clearTimeOut( ) : 取消setTimeout()函数
- cleaerInterval( ) : 取消setInterval函数
- window对象的方法，一般可以省略window对象，直接使用方法

```javascript
<head>
	<script type="text/javascript">
		function show1() {
			/*关闭当前页面*/
			close();
		}
		function show2() {
			/*打开一个新的浏览器窗口或查找一个已命名的窗口。*/
			window.open("http://www.baidu.com");
			//open("https://www.baidu.com/", "", "width=400,height=400", true);
		}
		/*setInterval():在间隔的毫秒后调用函数，一直调用*/
		/*setTimeout( ):在指定的毫秒后调用一次函数，只调用一回 */
		/*clearInterval()取消setInterval函数 */
		/*clearTimeout()取消setTimeout()函数*/
		function show3() {
			/*定时：调用一回*/
			a = setTimeout(function() {
				/*创建当前时间*/
				var now = new Date();
				/*document.getElementById("timeId")，获取timeId节点*/
				/*innerHTML：写内容*/
				document.getElementById("timeId").innerHTML = now;
			}, 5000);
		}
		function show30() {
			clearTimeout(a);
		}
		/*计时：一直调用*/
		function show4() {
			b = setInterval(function() {
				var now = new Date();
				document.getElementById("time").innerHTML = now.toLocaleString();
			}, 1000)
		}
		function show40() {
			clearInterval(b);
		}
	</script>
</head>
<body>
	<a href="javascript:close()">关闭</a>
	<button onclick="show1()">关闭</button>
	<button onclick="show2()">打开</button>
	<div id="container">
		<p><span>时间：</span><span id="timeId"></span></p>
		<button onclick="show3()">我3秒后显示时间</button>
		<button onclick="show30()">取消timeout</button>
		<p><span>时间：</span><span id="time"></span></p>
		<button onclick="show4()">每秒显示实时时间</button>
		<button onclick="show40()">取消Interval(停止当前时间)</button>
	</div>
</body>
```

## 15.时间

```
<script type="text/javascript">
var now = new Date();
document.write(now + "<br/>");
document.write(now.getYear() + 1900 + "<br/>");
document.writeln(now.getFullYear()+"<br/>");
document.write(now.getMonth() + 1 + "<br/>");
document.write(now.getDate() + "<br/>");
document.write(now.getHours() + "<br/>");
document.write(now.getMinutes() + "<br/>");
document.write(now.getSeconds() + "<br/>");
document.write(now.toLocaleString() + "<br/>");
document.write(now.toLocaleDateString() + "<br/>");
document.write(now.toLocaleTimeString() + "<br/>");
document.write(now.toString() + "<br/>");
/*时间戳*/
var tagetTime = Date.parse(new Date("2017-10-1"));
document.writeln(typeof(tagetTime));
document.writeln(tagetTime);
</script>
```

## 16. DOM 文档对象模型

### 16.1属性

- URL:         返回当前文档的URL
- referrer : 返回载入当前文档的来源(百度推广)

### 16.2方法

- getElementById("id名称")
  - value=值		向控件的value属性赋值`<input type="text" value="张三">`
  - innerText=值         向控件标签之间赋值,`<b>xxx</b>`输出xxx
  - innerHTML=值     向控件标签之间赋值,`<b>xxx</b>`输出加粗后xxx
- getElementsByName("") 根据控件的name名称找到一组元素
- getElementsTagName("")根据控件的标签名称找到一组元素
- write()   向正文输出内容 
- writeln() 向正文输出内容，内容后加上空格 

```html
<script type="text/javascript">
    document.write(window.document.URL + "<br/>");
    document.write(window.location.href + "<br/>");
 	document.write(document.referrer);
    function changeDiv() {
        document.getElementById("node").innerHTML = "<font color='red'>网易</font>";
    }
    function showSeason() {
        var es = document.getElementsByName("season");
        var arr = new Array();
        for (var i = 0; i < es.length; i++) {
            arr.push(es[i].value);
        }
        document.getElementById("s").innerHTML = arr.join("-");
    }
    function showInput() {
        var is = document.getElementsByTagName("input");
        document.getElementById("s").innerHTML = is.length;
    }
    </script>
</head>

<body>
    <input name="b1" type="button" value="改变层内容" onclick="changeDiv()" />
    <div id="node">新浪</div>
    <hr />
    <input name="season" type="text" value="春" />
    <input name="season" type="text" value="夏" />
    <input name="season" type="text" value="秋" />
    <input name="season" type="text" value="冬" />
    <br />
    <input name="b2" type="button" value="显示input内容" onclick="showInput()" />
    <input name="b3" type="button" value="显示season内容" onclick="showSeason()" />
    <p id="s"></p>
</body>
```

## 17.DOM节点详解

### 17.1. 节点的类型

- 元素节点
- 属性节点
- 文本节点

### 17.2. 获取元素节点

- document.getElementById(" ")
- document.getElementsByName(" ")
- document.getElementsByTagName(" ")

```html
<script type="text/javascript">
    window.onload = function() {
        var bjNode = document.getElementById("bj");
        console.info(bjNode);
        var liNodes = document.getElementsByTagName("li");
        console.info(liNodes.length);
        var liNodes2 = document.getElementById("city").getElementsByTagName("li");
        console.info(liNodes2.length);
        var genderNodes = document.getElementsByName("gender");
        console.info(genderNodes.length);
    }
    </script>
</head>

<body>
    <p>你喜欢的城市</p>
    <ul id="city">
        <li id="bj" name="beijing">北京</li>
        <li>上海</li>
        <li>广州</li>
        <li>深圳</li>
    </ul>
    <br/>
    <br/>
    <p>你的喜欢的游戏</p>
    <ul id="game">
        <li id="rl">红警</li>
        <li>连连看</li>
        <li>扫雷</li>
        <li>纸牌</li>
    </ul>
    <br/>
    <br/> gender:
    <input type="radio" name="gender" value="male">男
    <input type="radio" name="gender" value="female">女
</body>
```

### 17.3. 获取属性节点(节点属性)

- 通过元素节点.属性名来获取,属性名=值;
- 通过元素节点.getAttributeNode()来获取，再通过nodeValue来读写属性值;

```html
<script type="text/javascript">
   window.onload = function() {
     var nameNode = document.getElementById("name");
     //属性节点操作
     //nameNode.value = "张三丰";

     var valueAttr = nameNode.getAttributeNode("value");
     valueAttr.nodeValue = "张三丰2"
   }
</script>
```

### 17.4.获取元素节点的子节点

- childNodes : 当前元素节点下所有子节点(注意换行也属子节点)
- firstChild : 获取第一个子节点
- lastChild ：获取最后一个子节点

```javascript
window.onload = function() {
  var cityNode = document.getElementById("city");
  //city元素下所有子节点，注意9点，4个li+5个换行
  var nodes = cityNode.childNodes;
  console.info(nodes.length);
  console.info(cityNode.firstChild);
  console.info(cityNode.lastChild);
}
<p>你喜欢的城市</p>
<ul id="city">
  <li id="bj" name="beijing">北京</li>
  <li>上海</li>
  <li>广州</li>
  <li>深圳</li>
</ul>
```

### 17.5.获取文本节点

元素节点--》元素节点的子节点：取文本节点的值nodeValue

```html
<script type="text/javascript">
  window.onload = function() {
    var bjNode = document.getElementById("bj");
    var textNode = bjNode.firstChild;
    textNode.nodeValue = "南京";
    console.info(textNode.nodeType + "-" + textNode.nodeValue);
    //innerHTML、innerText不是标准的DOM规范
    //bjNode.innerHTML = "大南京";
  }
</script>
<p>你喜欢的城市</p>
<ul id="city">
  <li id="bj" name="beijing">北京</li>
  <li>上海</li>
  <li>广州</li>
  <li>深圳</li>
</ul>
```

### 17.6. 节点的属性

- nodeName:属性名
  - 只读属性：如果是文本节点，返回#text
- nodeType:属性类型
  - 只读属性
  - 1--元素节点
  - 2 -- 属性节点
  - 3-- 文本节点
- nodeValue: 返回当前节点的值
  - 读写属性
  - 元素节点，返回值是null
  - 属性节点，返回值是属性值
  - 文本节点，返回值是文件值

```javascript
 window.onload = function() {
        //元素节点
        //nodeName
        //nodeType
        //nodeValue:null
        var bjNode = document.getElementById("bj");
        console.info(bjNode.nodeName); //li
        console.info(bjNode.nodeType); //1
        console.info(bjNode.nodeValue); //null

        //属性节点
        var nameAttr = document.getElementById("bj").getAttributeNode("name");
        //nodeName
        //nodeType
        //nodeValue
        console.info(nameAttr.nodeName); //name
        console.info(nameAttr.nodeType); //2
        console.info(nameAttr.nodeValue); //beijing

        //文本节点
        var textNode = document.getElementById("bj").firstChild;
        //nodeName:#text
        //nodeType
        //nodeValue
        console.info(textNode.nodeName); //#text
        console.info(textNode.nodeType); //3
        console.info(textNode.nodeValue); //北京
    }
 
 <p>你喜欢的城市</p>
 <ul id="city">
   <li id="bj" name="beijing">北京</li>
   <li>上海</li>
   <li>广州</li>
   <li>深圳</li>
   </ul>
```

### 17.7. 创建一个元素节点

- createElement();

### 17.8. 创建一个文本节点

- createTextNode();

### 17.9. 创建一个元素子节点

- appendChild();

### 17.10. 创建一个属性节点并赋值

- createAttribute()

- 设置元素的属性  setAttributeNode(xxx);

  <p>你喜欢的城市</p>

  ```
  <script type="text/javascript">
      window.onload = function() {
          //创建元素 createElement();
          var liNode = document.createElement("li");

          //创建属性  createAttribute();
          var idAttr = document.createAttribute("id");
          idAttr.nodeValue = "nj";
          //创建文本  createTextNode();
          var txtNode = document.createTextNode("南京");

          //把属性加入到li元素中
          liNode.setAttributeNode(idAttr);
          //把文本加入到li元素中增加子元素  appendChild();
          liNode.append(txtNode);

          //把liNode元素节点加入city元素节点
          document.getElementById("city").appendChild(liNode);
      }
  </script>
  <ul id="city">
      <li id="bj" name="beijing">北京</li>
      <li>上海</li>
      <li>广州</li>
      <li>深圳</li>
  </ul>
  ```

### 17.11. 节点替换

- replaceChild();

### 17.12. 插入节点

- insertBefore();

### 17.13. 删除

- removeChild();

```html
<script type="text/javascript">
  window.onload = function() {
    var bjNode = document.getElementById("bj");
    var rlNode = document.getElementById("rl");
    //var liNode = document.createElement("li");
    //liNode.append('xxxx')

    var cityNode = document.getElementById("city");
    //替换
    cityNode.replaceChild(rlNode, bjNode)

    //插入
    var liNode = document.createElement("li");
    liNode.append('xxxx')
    var llkNode = document.getElementById("llk");
    document.getElementById("game").insertBefore(liNode, llkNode);

    //删除
    document.getElementById("game").removeChild(llkNode);
  }
</script>
<body>
    <p>你喜欢的城市</p>
    <ul id="city">
        <li id="bj" name="beijing">北京</li>
        <li>上海</li>
        <li>广州</li>
        <li>深圳</li>
    </ul>
    <br/>
    <br/>
    <p>你的喜欢的游戏</p>
    <ul id="game">
        <li id="rl">红警</li>
        <li id="llk">连连看</li>
        <li>扫雷</li>
        <li>纸牌</li>
    </ul>
    <br/>
    <br/> gender:
    <input type="radio" name="gender" value="male">男
    <input type="radio" name="gender" value="female">女
</body>
```

## 18. 创建对象

- new Date()
- new String()
- 要求创建Student对象

### 18.1. 用Object构造函数来创建一个对象

```javascript
	// var str = new String("abc");
    // document.write(str + "<br/>");
	
	//1.用Object构造函数来创建一个对象
    var stu = new Object();
    //属性
    stu.id = 1001;
    stu.name = "张三丰";
	stu['name'] = "张三丰";

    //方法
    stu.study = function() {
        document.write("好好学习，天天向上<br/>");
    }

    //调用属性
    document.write(stu.id + "-" + stu.name + "<br/>");
    //调用方法
    stu.study();
```

### 18.2. 通{}创建json对象

```javascript
//2.用{}创建对象
/*var stu2 = {};
    stu2.id = 1001;
    stu2.name = "张三丰";*/
var stu2 = {
  "id": "1001",
  "name": "张三丰",
  "study": function() {
    document.write("好好学习，天天向上<br/>");
  }
};
stu2.id = 101;
document.write(stu2.id + "-" + stu2['name'] + "<br/>");
//调用方法
stu2.study();
```

虽然Object 构造函数和{} 都可以用来创建单个对象，

但这些方式有个明显的缺点：创建同一类型多个对象，会产生大量的重复代码。为解决这个问题，人们开始使用工厂模式的一种变体。

### 18.3. 工厂模式

```javascript
 //3.工厂模式
 function createStudent(id, name) {
   var o = new Object();
   o.id = id;
   o.name = name;
   o.study = function() {
   document.write("好好学习，天天向上<br/>");
   }
   return o;
 }
 var stu11 = createStudent(1001, "张三");
 var stu12 = createStudent(1003, "李四");
 document.write(stu11.id + "-" + stu11['name'] + "<br/>");
 stu11.study();
 document.write(stu12.id + "-" + stu12['name'] + "<br/>");
 //调用方法
 stu12.study();
 document.write("<hr/>");
```

工厂模式虽然解决了创建多个相似对象的问题，但却没有解决对象识别的问题（即怎样知道一个对象的类型）。随着JavaScript 
的发展，又一个新模式出现了。

### 18.4. 构造函数模式

```javascript
//4. 构造函数模式
    function Student(id, name) {
        this.id = id;
        this.name = name;
        this.study = function() {
            document.write("好好学习，天天向上<br/>");
        }
    }
    var stu21 = new Student(1001, "张三");
    var stu22 = new Student(1003, "李四");
    document.write(stu21.id + "-" + stu21['name'] + "<br/>");
    stu21.study();
    document.write(stu22.id + "-" + stu22['name'] + "<br/>");
    //调用方法
    stu22.study();
    document.write("<hr/>");
```

缺点每个对象都会创建新的study函数

### 18.5. 构造函数模式改良

```javascript
//5. 构造函数模式 改良
function Student(id, name) {
  this.id = id;
  this.name = name;
  this.study = study;
}

function study() {
  document.write("好好学习，天天向上<br/>");
}
```




















