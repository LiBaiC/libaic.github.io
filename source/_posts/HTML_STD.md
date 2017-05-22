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

### 布局
&lt;style&gt;
&lt;/style&gt;
在style内布局,常见元素
```
divName
{
	填充元素
}
```
* float:left/right         			 左右排列对齐;
* clear:left/right/both;			 清楚左/右对齐;
* background:red/black...;           区域背景颜色;
* width:100px ,height:100px;		 区域长宽;
* margin/margin-top/margin-bottom/margin-left/margin-left;  边界间隔;

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


### 盒模型


### 补充
1. Html注释:&lt;!--&gt;balabala...&lt;--&gt;;