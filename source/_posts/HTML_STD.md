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
### 补充
1. Html注释:&lt;!--&gt;balabala...&lt;--&gt;;
2. 相邻的普通元素，上下间距，并非简单的相加，而是取较大的边距值，这种现象叫做margin重叠