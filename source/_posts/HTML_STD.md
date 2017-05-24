# HTML学习
## 定义
HTML指的是超文本标记语言(Hyper Text Markup Language)

## 格式
&lt;doctype&gt; : 严格、过度、松散标准
### ps:使用Sublime可以快速生成模板,主要有一下几种方法：
输入

* html:4t
* html:4s
* html:xs
* html:xt
* html:XXS
* html:5

按下回车即可生成相应约束模板。

&lt;html&gt;
&lt;head&gt; : 写给机器看
&lt;body&gt; : 内容

### div&css
通俗比喻div声明几个区块,css来定义这块地有多大。div布局,css控制

## DIV布局

### 布局元素
&lt;style&gt;
&lt;/style&gt;
在style内布局,常见元素
```
divName
{
	填充元素
}
```

##### 1.块状元素
独占块状区域

* float:left/right         			 左右排列对齐;
* clear:left/right/both;			 清楚左/右对齐;
* background:red/black...;           区域背景颜色;
* width:100px ,height:100px;		 区域长宽;
* margin/margin-top/margin-bottom/margin-left/margin-left;  边界间隔;
* margin： auto;可实现居中;
* padding							 内边距;

定义一个div类

```
<div class = "dClass"></div>
```
在style内布局

```
.dclass
{
	//统一对某一类div设置
}
```

##### 2.内联元素
内联元素,只对每一行的文字起作用,或者说内联的作用范围不能跳出行的区域。
1.span
```
<span>
exp: 
//沧海两个字会被渲染成红色
<style>
	#word{
		color:red;
	}
</style>

<div>
	长风破浪会有时，直挂云帆济<span id ="word">沧海</span>。<br/>
</div>
```

### 块状和内联的转换
可以使用强制转换:
display: block/inline/none;
强制转化为：块状、内联、删除

## CSS控制段落文本

### 1.CSS控制字体大小颜色
```
<style>
	#p1{
			background:blue;
			text-indent:20px;
			text-align:center;               //居中
			text-decoration:line-through;    //对文字添加效果:删除线
			letter-spacing:2px;				 //文字间距离	
			color:blue;						 //字体颜色
			//PS 可以用font:italic bold 23px/46px "SimHei"一行代替一下（顺序不能改变）
			font—style:italic;               //斜体
			font-weight:bold;			     //加粗
			font-size:23px;                  //大小
			line-height:46;                  //行距
			font-family:"SimHei";            //字体
		}
</style>
<p id = "p1">中间适用一个文字段落</p>
```

### 2.背景图片

```
<style>
	<body>
		background-color:blue;
		background-image:url(small.jpg)
		background-repeat:no-repeat        //背景图片不平铺
		background-position:center right;   //
	</body>
</style>
```

### 3.CSS选择器
* Id选择器
* class选择器
* 标签选择器
* 派生选择器
```
<style>
	#test1{
			width:100px;
			height:50px;
			border:1px solid blue;
		}	
	.test2{
			width:100px;
			height:50px;
			border:1px solid red;
		}
	div{
			width:100px;
			height:50px;
			background:orange;
		}	
	div p{                      //只会影响div下的p标签，不会影响独立p标签
			color：red; 
		}
</style>
<head>
	<body>
		<div id = "test1">test1</div>
		<div class ="test2"> </div>	
		<div> 普通div
			<p> 我是div中的p标签</p>
		<p>我是独立p标签</p>
	<body>
</head>
```
### 4.CSS的优先级
标签选择器(p)<类选择器(class)<Id选择器(#test1)<派生选择器
控制的越精细，优先级越高

### 5.CSS引入方式
1. 直接写在头部文件里
```
<style>
	body{
			background:blue;
		}
</style>
<head>
	<body>
	</body>
</head>
```
2. 单独定义css文件
```
1.新建一个css文件：newCSS.css
2.编写css #test{
			width:200px;
			height:200px;
			background:red;
			}
3.在HTML加入css文件引用
<link rel="stylesheet" href="./newCss.css">             //href后面为css文件的路径
```

3.直接在HTML标签里写入对这个标签的CSS控制
```
<div style="border:1px solid red;"> 测试</div>
``` 

4.有多个css文件，可以导入
```
在一个css文件内应用其他css文件
@import url(xx.csss);
```

### 6.CSS初始化
css代码之所以初始化，是因为能尽量减少 各浏览器之间的兼容性问题!
```
<head>
  <style>
    ul{border:2px solid blue;}
    li{border:5px bolid green; }
  </style>
</head>
<body>
  <div>相同的元素，如li，在不同的浏览器下，显示的效果稍有不同。<br/>
       因为浏览器对各元素的margin，border，font-size等略有不同。<br/>
       为杜绝这种情况发生，可通过CSS强制其所有元素的属性值都一样。<br/>
       则浏览器显示就一致了，减少了不兼容情况的发生。该过程即为CSS初始化。<br/>
    <ul>
       <li>a</li>
       <li>b</li>
       <li>c</li>
       <li>d</li>
    </ul>
  </div>
</body>


淘宝官网 样式初始化
1.body, h1, h2, h3, h4, h5, h6, hr, p, blockquote, dl, dt, dd, ul, ol, li, pre, form, fieldset, legend, button, input, textarea, th, td { margin:0; padding:0; } 
2.body, button, input, select, textarea { font:12px/1.5tahoma, arial, \5b8b\4f53; } 
3.h1, h2, h3, h4, h5, h6{ font-size:100%; } 
4.address, cite, dfn, em, var { font-style:normal; } 
5.code, kbd, pre, samp { font-family:couriernew, courier, monospace; } 
6.small{ font-size:12px; } 
7.ul, ol { list-style:none; } 
8.a { text-decoration:none; } 
9.a:hover { text-decoration:underline; } 
10.sup { vertical-align:text-top; } 
11.sub{ vertical-align:text-bottom; } 
12.legend { color:#000; } 
13.fieldset, img { border:0; } 
14.button, input, select, textarea { font-size:100%; } 
15.table { border-collapse:collapse; border-spacing:0; } 

```

### 补充
1. Html注释:&lt;!--&gt;balabala...&lt;--&gt;;
2. 相邻的普通元素，上下间距，并非简单的相加，而是取较大的边距值，这种现象叫做margin重叠