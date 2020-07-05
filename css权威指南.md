# 第八章 内边距，边框，轮廓和外边距

# 第十章 浮动及其形状
# 第十一章 定位
# 第十二章 弹性盒布局
# 第十三章 栅格布局
# 第十四章 CSS中的表格布局
# 第十五章 列表和生成的内容
# 第十六章 变形
# 第十七章 过渡
# 第十八章 动画
# 第十九章 滤镜,混合,裁剪和遮罩
# 第二十章 针对特定媒体的样式
# 第一章 CSS和文档
## 元素
在css中元素有两种形式  
 1. 置换元素
 2. 非置换元素  

如果按照显示方法来区分也分为两种
 1. 块级元素
 2. 行内元素

块级元素里可以放行内元素，行内元素不能放块级元素

##媒体查询
元素：@media专门用来查询媒体
```css
//简单的查询
@media all{
	h1{color:red;}
	body{background:yellow;}
}

*{
    margin: 0;
    padding: 0;
}
@media(max-width:900px){
    div{
        width: 500px;
        height: 500px;
        background-color: red;
    }
}
@media(min-width:1200px){
    div{
        width: 500px;
        height: 500px;
        background-color: blue;
    }
}
```
多个特性描述符用and连接，媒体查询中用的关键词有两个：
 1. and
 2. not 注意not必须要在媒体查询开头使用 (color) and not (min-device-width:800px)这样写是错误的，浏览器会忽略

媒体查询不支持or，但是可以用","逗号来表示和or相同的效果
## 特性查询
```css
//如果浏览器支持supports里面的就应用里面的
@supports(color:black){
	body{color:black;}
	h1{color:purple;}
	h2{color:navy;}
}
```
特性查询还可以支持嵌套同时也可以使用逻辑判断and，not  
**记住这是特性查询而不是正确性查询**
# 第二章 选择符
## 选择符
 1. 元素选择符 h1{}
 2. 群组选择符 h1,h2{}
 3. 类选择器 .h1{} (类选择器可以是多个字，词之间用空格分开)
 4. id选择器 #h1{} (id选择器只能用一个)
 
## 属性选择符
 1. 简单选择符
 2. 精准选择符
 3. 部分匹配选择符
 4. 起始值属性选择符

简单属性选择符：选择的元素具有某个属性，而不管属性的值是什么	h1[class]{}  
精准选择符：在简单选择符的基础上限制属性值 h1[class=h1]{}
部分属性选择符：根据属性值的一部分选择元素，而不是完整的值
```css
//选择的元素有class属性，而且属性值开头是h1加一个英文破折号“-”或者就是h1本身(h1-good)可以
h1[class|='h1']{}
//选择的元素有class属性，而且属性值是包含'h1'的一组词（good h1 hah)可以
h1[class~='h1']{}
//选择的元素有class属性，而且属性值中包含h1（faafh1fafa)可以
h1[class*='h1']{}
//选择的元素有class属性，而且属性值以h1开头（h1fafafa)可以
h1[class^='h1']{}
//选择的元素有class属性，而且属性值以h1结尾 (fafah1)可以
h1[class$='h1']{}
```
**在css的属性选择符中加入了不区分大小写的选项，只需在最后加入i就可以了**  
```css
a[href$='.pdf' i]
```

**注意：只能在属性选择符中使用i**

## 根据文档结构选择
 1. 后代选择符
 2. 子元素选择符
 3. 紧邻同胞选择符
 4. 后续同胞选择符

```css
//后代选择符
h1 em{}
//子代选择符
h1>em{}
//紧邻同胞选择符(h1和p拥有同一个父类，而且p紧跟在在h1之后被定义)
h1+p
//后续同胞选择符(h1和p拥有同一个父类，但p不一定需要紧跟在h1之后被定义，只要在h1之后定义就行）
h1~p{}

```
## 伪类选择符
 1. 拼接伪类
 2. 结构伪类
 	 1. 选择根元素(:root 在html中，根元素永远是html)
 	 2. 选择空元素(:empty)
 	 3. 选择唯一的子代(only-child)
 	 4. 选择第一个和最后一个子代(:first-child , last-child)
 	 5. 选择第一个和最后一个某种元素(first-of-type last-of-type)
 	 6. 选择第n个子元素(:nth-child() :nth-last-child())
 	 7. 选择第n给某种元素(nth-of-type() nth-last-of-type())
 3. 动态伪类	
 	 1. 超链接伪类(:link :visited)
 	 2. 用户操作伪类(:focus :hover :active)
 5. UI状态伪类
 	 1. 默认选择伪类(:default)
 	 2. 可选性伪类(:required)
 	 3. 有效性伪类(:valid)
 	 4. 范围伪类(:in-range out-of-range)
 	 5. 可变性伪类(:read-write read-only)
 6. :target伪类
 7. :lang伪类(可以根据文本使用的语言选择元素）
 8. 否定伪类（:not()用来否定)

```css
<!--结构伪类-->
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title></title>
		<style type="text/css">
			:root{
				margin: 0;
				padding: 0;
			}
			
			div:empty{
				width: 250px;
				height: 250px;
				background-color: blue;
			}
			.only-child p:only-child{
				color:red;
			}
			.list h1:nth-child(3){
				color:red;
			}
			.list p:nth-of-type(2){
				color:blue;
			}
		</style>
	</head>
	<body>
		<div></div>
		<div class="only-child">
			<p>This Is P</p>
		</div>
		<div class="list">
			<h1>This is H1</h1>
			<p>This Is P</p>
			<h1>This is H1</h1>
			<p>This Is P</p>
			<h1>This is H1</h1>
			<p>This Is P</p>
			<h1>This is H1</h1>
			<p>This Is P</p>
			<h1>This is H1</h1>
			<p>This Is P</p>
			<h1>This is H1</h1>
			<p>This Is P</p>
			
		</div>
	</body>
</html>

```
```css
<!-- 超链接伪类 -->
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title></title>
		<style type="text/css">
			a:link{
				color:red;
			}
			a:visited{
				color:yellow;
			}
		</style>
	</head>
	<body>
		<a href="#">百度一下</a>
	</body>
</html>

```
```css
<!-- 用户操作伪类 -->
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title></title>
		<style type="text/css">
			input:focus{
				background-color: red;
			}
			div:hover{
				color:blue;
			}
			a:active{
				color:green;
			}
		</style>
	</head>
	<body>
		<a href="#">百度</a>
		<div id="">
			点一下试试
		</div>
		<input type="text" name="" id="" value="" />
	</body>
</html>

```
```css
<!-- UI状态伪类 -->
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title>UI伪类选择器</title>
		<style type="text/css">
			/* 不允许编辑 */
			input:disabled{
				background-color: red;
			}
			/* 默认的 */
			input[type='radio']:default{
				height: 20px;
				width: 20px;
			}
			/* 指代用户选择的复选框或者单选按钮,默认的也可以应用上 */
/* 			input[type='radio']:checked{
				height: 30px;
				width: 30px;
			} */
			/* 必填的 */
			input:required{
				background-color: #FFFF00;
			}
			/* 超过规定范围后 */
			input:out-of-range{
				background-color: red;
			}
			/* 在规定范围中时 */
			input:in-range{
				background-color: aqua;
			}
			/* 读写标签 */
			input[class='read']:read-write{
				background-color: aquamarine;
			}
			p:read-only{
				color:red;
			}
			/* 表示接受输入的元素 */
			input[class='enabled']:enabled{
				background-color: red;
			}
			/* 代表用户输入有效数据时 */
			input[id='range']:valid{
				width: 200px;
				height: 20px;
			}
			/* 代表用户输入的数据不在规定范围内时 */
			input[id='range']:invalid{
				width: 300px;
				height: 30px;
			}
			/* 代表用户无需一定填的 */
			input[class='bixu']:optional{
				background-color: #00FFFF;
			}
		</style>
	</head>
	<body>
		<form action="#" method="post">
			<input type="text" name="" id="" value="允许输入文本" />
			<input type="" name="" id="" value="不允许输入文本" disabled="disabled" />
			<input type="radio" name="radio" id="" value=""  />
			<input type="radio" name="radio" id="" value="" checked="checked" />
			<input type="text" name="" id="" value="必须填的项目" required="required"/>
			<input type="number" name="" id="" value="请填写1-100的数字" min="1" max="100"/>
			<input type="text" name="" class="read" value="" />
			<p contenteditable="true">THis is p</p>
			<p>THis is p</p>
			<input type="text" name="" class="enabled" value="" />
			<input type="text" name="" class="enabled" value="" />
			<input type="number" name="" id="range" value="1" min="1" max="1000" />
			<div id="">
				<input type="text" name="" class="bixu" value="" required="required"/>
				<input type="text" name="" class="bixu" value="" />
			</div>
			<button type="button">提交</button>
		</form>
	</body>
</html>
<!-- UI状态伪类 -->
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title>UI伪类选择器</title>
		<style type="text/css">
			/* 不允许编辑 */
			input:disabled{
				background-color: red;
			}
			/* 默认的 */
			input[type='radio']:default{
				height: 20px;
				width: 20px;
			}
			/* 指代用户选择的复选框或者单选按钮,默认的也可以应用上 */
/* 			input[type='radio']:checked{
				height: 30px;
				width: 30px;
			} */
			/* 必填的 */
			input:required{
				background-color: #FFFF00;
			}
			/* 超过规定范围后 */
			input:out-of-range{
				background-color: red;
			}
			/* 在规定范围中时 */
			input:in-range{
				background-color: aqua;
			}
			/* 读写标签 */
			input[class='read']:read-write{
				background-color: aquamarine;
			}
			p:read-only{
				color:red;
			}
			/* 表示接受输入的元素 */
			input[class='enabled']:enabled{
				background-color: red;
			}
			/* 代表用户输入有效数据时 */
			input[id='range']:valid{
				width: 200px;
				height: 20px;
			}
			/* 代表用户输入的数据不在规定范围内时 */
			input[id='range']:invalid{
				width: 300px;
				height: 30px;
			}
			/* 代表用户无需一定填的 */
			input[class='bixu']:optional{
				background-color: #00FFFF;
			}
		</style>
	</head>
	<body>
		<form action="#" method="post">
			<input type="text" name="" id="" value="允许输入文本" />
			<input type="" name="" id="" value="不允许输入文本" disabled="disabled" />
			<input type="radio" name="radio" id="" value=""  />
			<input type="radio" name="radio" id="" value="" checked="checked" />
			<input type="text" name="" id="" value="必须填的项目" required="required"/>
			<input type="number" name="" id="" value="请填写1-100的数字" min="1" max="100"/>
			<input type="text" name="" class="read" value="" />
			<p contenteditable="true">THis is p</p>
			<p>THis is p</p>
			<input type="text" name="" class="enabled" value="" />
			<input type="text" name="" class="enabled" value="" />
			<input type="number" name="" id="range" value="1" min="1" max="1000" />
			<div id="">
				<input type="text" name="" class="bixu" value="" required="required"/>
				<input type="text" name="" class="bixu" value="" />
			</div>
			<button type="button">提交</button>
		</form>
	</body>
</html>

```
```css
<!-- :lang选择符和:not()否定选择符 -->
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title></title>
		<style type="text/css">
			p:lang(cn){
				color: red;
			}
			a:target{
				color:red
			}
			p:not([class='p']):not(.maxin){
				color: red;
			}
		</style>
	</head>
	<body>
		<div>
			<p lang="en">This is p</p>
			<p lang="en">This is p</p>
			<p lang="cn">这是p</p>
			<p lang="en">This is p</p>
			<p lang="en">This is p</p>
		</div>
		<div>
			<a href="http://www.baidu.com/#target-pseudo" target="_blank">百度一下</a>
			<a href="http://www.baidu.com">百度两下</a>
		</div>
		<div>
			<p class="p">This is p</p>
			<p class="p">This is p</p>
			<p class="maxin">THis is p</p>
			<p>This is p</p>
			<p class="maxin">THis is p</p>
			<p class="p">This is p</p>
			<p class="p">This is p</p>
		</div>
	</body>
</html>

```
**UI状态伪类总结**
1. :enabled 指代接受输入的元素
2. :disabled 指代不允许输入的元素
3. :checked 指代用户选中的单选按钮或复选框
4. :default 指代默认选择的单选按钮，复选框之类的
5. :valid 指代满足**所有**数据有效性的输入框
6. :invalid 指代不满足**所有**数据的输入框
7. :in-range 指代输入的值在最大值和最小值之间的
8. :out-of-range 指代输入的数据超过最大值或最小值的
9. :required 指代必须输入的输入框
10. :optional 指代无需一定要输入值的输入框
11. ：read-write 指代能读写的元素(表单元素中设置了disabled属性就是只读属性了）
12. ：read-only 指代只能读的元素(在html中，绝大部分元素都是只读元素，除非使用contenteditable属性来转换为可编辑元素)
13. ：indeterminate **我也没搞懂，学完js在来看看**
##伪元素选择符
 1. ::first-letter(装饰首个字母,只能运用到块级元素)
 2. ::first-line(装饰首行，只能运用到块级元素)
 3. ::before ::after(装饰前置和后置内容元素)
```css
		<style type="text/css">
			/* 装饰首字母 */
			p::first-letter{
				display: block;
				width: 50px;
				height: 50px;
				color:red;
			}
			/* 装饰第一行 */
			div::first-line{
				color:blue;
			}
			/* 不能运用到行内元素 */
			a::first-letter{
				color:yellow;
			}
			div[class='hi']::before{
				content: ']]';
				color:silver;
			}
		</style>
	<body>
		<p>this is p</p>
		<div>
			afafafafafafafafafafafafafafafafafafafafafafafaf
		</div>
		<a href="#">百度</a>
		<div class="hi">
			看看我前面是不是有东西呀
		</div>
	</body>	
```

# 第三章 特指度和层叠
## 特指度
- 选择符中每多一个id属性加0,1,0,0
- 选择符中每一个类属性值，属性选择或伪类加0,0,1,0
- 选择符中每个元素和伪元素加0,0,0,1。
- 连接符和通用选择符不加特制度
- 直接在元素标签中定义的加1,0,0,0

## 继承
多数盒子模型的属性都不会被继承，包括margin,padding,background,border  
**继承的值没有特指度，连0都没有。没有特制度和特制度为0是两个不同的概念**  
**0特指度战胜无特制度**
## 层叠
如果两个特制度相同的规则应用到同一个元素会发生什么？默认情况下层叠的规则如下  
1. 找到匹配的指定元素和所有规则
2. 有!important的规则比没有!important的高
3. 按照声明的前后应用，靠后的声明权重高
#第 四章 值和单位
## 关键词
css3定义了几个全局关键词：inherit，initial和unset  
inherit的意思是将元素的属性设置为和父类相同，即使这个属性不会被继承！  
initial的意思是设置元素的属性为初始值，不过不是所有属性都有初始值！！！  
unset是inherit和initial的通用替身，对继承的元素来说unset和inherit的作用一样，对不继承的元素来说unset的作用和initial一样
## 单位  
在css中长度单位分为两种：
 - 绝对长度单位
	1. in(英寸）【一英寸等于2.54厘米】
	2. cm（厘米）【一厘米等于0.394英寸】
	3. mm（毫米）【一英寸等于25.4毫米，1毫米等于0.0394英寸】
	4. q（四分之一毫米）【一厘米有40个q单位】
	5. pt（点）【一英寸有72个点】
	6. pc（派卡）【一派卡等于12点】
	7. px（像素）【一英寸能放96个像素】
 - 相对长度单位
 	1. em【按照css定义，em是按照font-size决定的，如果font-size为14px，那么1em和ex为14px】
 	2. ex【ex指所用字体中小写字母x的高度】

在css中提供了calc()来做简单的计算，但是要注意：
	1. +和-两侧必须使用相同的单位类型，或者两边都没有单位也可以，符号两边要有空格
	2. *法计算两侧中必须有一个是数字（不能带符号），2.5px * 2px就是错的，应为它等于5px²
	3. /法计算右边的值必须是数字（不能带符号）
###角度
角度单位有以下几种（通常在动画中使用）：
	1. deg（度数）
	2. grad（百分度，一个完整的圆周是400百分度）
	3. rad（弧度，完整的圆周是2Π，近似于6.28）
	4. turn（圈数）

### 时间和频率
	1. s（秒）
	2. ms（毫秒）

### 自定义属性
```css
	html{
    --co:blue;
    --wi:24px;
}
.bigbox{
    width: 300px;
    height: 900px;
    background-color:var(--co);
}
```
在css中自定义属性用两个--定义，如果要使用只需要使用var()方法，自定义属性区分大小写

### 位置
***我没看懂是什么意思***

# 第五章 字体
字体分为以下几种：
	- 衬线字体（字体宽度不同，有衬线）
	- 无衬线字体（字体宽度各异，但没有衬线 sans-serif）
	- 等宽字体（字体宽度相同）
	- 草书字体（模仿人类手写文字）
	- 奇幻字体

**在进行font-family字体设置时请指定几款通用的字体族，这样相当于提供了一种后备机制**
**在进行字体定义时，请加引号**
```css
font-family: "Cambria, Cochin", "Georgia", "Times", 'Times New Roman', serif;
```

### 使用@font-face
如果你想用一款字体，但没有在用户客户端安装，那么@font-face的作用就来了  
在@font-face中，font-family和src这两个是必须的！！！  
在定义好字体后，就可以在css中使用了(如果能设置一个备用字体链接就更好了）
```css
@font-face{
    font-family: 'lindaxia';
    src: url(./XiaoDouDaoHeiTangJian-2.ttf)
		 url（备用链接）;
}
h1{
    font-family: 'lindaxia';
}
```

如果想让浏览器知道所用的字体是什么格式，那就可以使用format(),这样做的好处是浏览器会跳过不支持的字体格式，减小带宽，提升数度（不过现在主流浏览器都支持这些的）
```css
	值				格式
	embedded-opentype eot
	opentype 		 otf
	svg			   svg
	truetype		  ttf
	woff			  woff
```
也可以在@font-face里面加入local(),指定已经在浏览器中安装的字体，如果能找到就不用去下载字体了，同时这样方法也可以给本地的字体取别名！
```css
@font-face{
    font-family: 'lindaxia';
    src: local("微软字体“）
		 url(./XiaoDouDaoHeiTangJian-2.ttf)
		 url（备用链接）;
}
h1{
    font-family: 'lindaxia';
}
```
### 字体描述符
	- font-style	区分常规，倾斜和倾斜字形
	- font-weight	区分不同的字重
	- font-stretch	区分众多字体变形
	- unicode-range	定义指定字体中可用的字符范围

unicode-range这个描述符可以自定义字体应用到哪些字符上（这个有时间慢慢搞懂）
```css
	unicode-range: U+590-5FF; /*希伯来语字符*/
	unicode-range: U+4E00-9FFF,U+FF00-FF9F,U+30??; /*日语汉字，平假名，片假名 */
```

**下面给出一个比较标准的font-face语句（还差了unicode-range，所以个人绝对不是最标准）**
```css
	@font-face{
		font-family:'lindaxia';
		src:url("lindaxia.eot");
		scr:url("lindaxia.eot?#iefix") format("embedded-opentype"),
			url("lindaxia.woff") format("woff"),
			url("lindaxia.ttf") format("truetype"),
			url("lindaxia.svg#switzera_adf_regular") format("svg")
}
```

### 字重
字重越大，字体越黑
**字重的工作方式（100-900）**
在css中100表示最小，900表示最大。但这些数字不代表字重本身，CSS规范只是说，**每个数字对应的权重至少和前面的数字具有相同的权重**
因此100，200，300，400可能对应同样的变体，500，600可能对应同样的变体，700，800，900可能对应同样的变体  
一般400对应normal，700对应bold，其他数字不与font-weight关键词对应
**字重可以继承**
如果把一个元素的字重设置为bolder，浏览器首先要确定父元素的值是什么**-然后选择比继承的字重高一级的最小数字**，如果找不到就把字重设为下一个数字值，直到900.lighter则相反

```css
	p{font-weight:normal;}
	p em{font-weight:bolder;} /*文本为粗体，字重为700*/

	h1{font-weight:blod;}
	h1 b{font-weight:bloder;} /*如果没有更粗的字型，其值为800 */

	div{font-weight:100;} /*假设有”light“字型*/
	div strong{font-weight:bolder;} /*文本为常规字型，字重为400 */
```

- 如果500未定义，则与400相同
- 如果300未定义，则相比于400细的那个变体，如果没有则与400相同，100，200也是这样处理
- 如果600未定义，则相对于500黑的下一个变体，如果没有这样的变体，则与500一样，700，800，900也是这样处理的

### 字号
font-size的作用是为字体的方框提供一个尺寸，所以显示出来不可能是完全指定的大小
font-size提供了绝对大小值：xx-small,x-small,small,medium,large,x-large,xx-large这几个关键词没有固定的大小，而是相对的。关键词larger和smaller和font-weight中的lighter和blorder差不多，都是根据父类元素的字号增加或减少
**字号能继承**

### 字形
font-style有三个取值：italic，oblique，normal
在这里要搞懂倾斜体和倾斜的区别，简单来说倾斜除了字母倾斜外，字符本身也会变化，而倾斜体只是直体的倾斜版本

### 字体拉伸
font-stretch用来设置字体中**可能**具有较宽或较窄的字母形式（不过一般都没有，价格太贵了）

### 字距调整
字句font-kerning定义了字符之间相对位置的距离，列如ox和oc这两个字母的间距就不同  
**如果字体中带字距就可以用，没有用了也没有效果，亲测大部分字体都没有字距**  
**如果既要调整字距，又应用letter-spacing属性，正确的顺序是先调整字距，再调整letter-spacing，而不是反过来**

### 字体变形
**字体变形font-variant也是要看字体是否携带变体信息，如果携带了就可以用font-variant来调用**
font-variant有最经典的两个属性：normal(普通)和small-caps(小号大写字母)

### 字体特性
字体特性font-feature-settings属性从低层控制OpenType字体的哪些特性可以使用（OTF格式）
***感觉没啥用，跳过了***

### font属性（重点）
**font-size基于父元素计算，而line-height基于当前元素的font-size计算**
**font的前三个值相对宽松狠多，font-style,font-weight,font-variant可以无视顺序，如果一个属性是normal，甚至可以不用写出！**
**但是font-size后面两个属性严格很多，顺序必须是font-size,font-family，而且必须出现在font中，不能省略**

# 第六章 文本属性
font和text的区别：文本是内容，而字体是用来显示内容的。

## 缩进文本（text-indent）
text-indent属性可用在任何**块级元素**，不能用在任何行内元素或置换元素中（如图像），然而如果图像在块级元素第一行中，它将会随着其他文本一起后移。**缩进的长度可以是负数**
**text-indent会继承，所以很可能出现意想不到的情况**

## 文本对齐（text-align）
 **text-align只能用于块级元素，而且有继承性**
在CSS中，对于从左到右的语言，text-aalign默认值是left，从右到左默认值为right。纵向书写的语言left和right对应始边和终边
**center标签和text-align：center的区别：center标签不仅影响文本，还能把整个元素（如表格）居中显示，而text-align：center不控制元素的对其方式，*只影响元素的内容***
justify两端对齐文本，一行的两端都与父元素边界对齐，单词和字母之间的空白会做调整，从而保证每一行长度完全一致

## 对齐最后一行（text-align-last）
**适用于块级元素，有继承性**
**text-align-center有个有趣的现象，如果第一行也是最后一行，text-align-last比text-align优先级高（估计text-align-last指的更全面，所以优先级高）

## 行的高度（line-height)
**line-height适用于所有元素，有继承性**
很多时候我们都认为line-height能直接增加行高，这其实是错误的。line-height控制的是**行距**，**除字体高度之外在文本上方的额外空间**
**元素的行距等于font-size的计算结果减去line-height的计算结果，注意，*行距可能是负数*，行距分为两半，分别放到内容区上下部分**

```css
<body>
    <div>
        <p>
            Lorem ipsum dolor sit amet consectetur adipisicing elit. Esse, qui? Nihil velit aliquam consequatur obcaecati, labore necessitatibus, eos quisquam quaerat ipsa temporibus repellat. Nisi dolorum distinctio ratione vero nulla cum.
        </p>
    </div>
	<style>
		*{
    margin: 0;
    padding: 0;
	}
	body{
    font-size: 10px;
	}
	div{
    line-height: 1em;
	}	
	p{
    font-size: 18px;
	}		
	</style>
</body>
```
line-height使用单位后子元素继承时就会继承那个固定的值，从而引起异常，所以line-height基本不带单位，用纯数字，这样子类继承时就会根据那个数字来计算行高（如父类line-height为1.5，那么子类继承的就是font-size * 1.5）

## 纵向对其文本(vertical-align)
**vertical-align适用于行内元素和单元格，没有继承性(除了使用关键词之外还可以使用px单位)**
vertical-align:baseline强制元素的基线与父类的基线对齐，多数时候浏览器都是这样做的，但如果目标元素没有基线，那么就与父类的基线对齐
vertical-align：sub把元素放在下标处，而且低于父类基线
vertical-align：super把元素放在上标处，而且高于父类基线
vertical-align:bottom把元素所在的行内框的底边与行框的底边对齐
vertical-align：top作用与bottom相反

## 单词间距和字符间距(word-spacing,letter-sapcing)
**word-spacing专门用来修改单词之间的距离，数值可正可负。适用于所有元素，可以继承**
**letter-spacing专门用来修改字符间距，数值可正可负，可以继承**

## 文本转换(text-transform)
**text-transform专门用来转换字体大小写，适用于所有元素，有继承**
text-transform常有的属性值为uppercase,lowercase,capitalize,none

## 文本装饰（text-decoration）
**text-decoration专门用来给字体加下划线，上划线，中划线等，适用于所有元素，没有继承性**
text-decoration常用的值有underline，overline，line-through，blink（让文本一闪一闪的，但是我没有这种效果啊！）
**虽然text-decoration不会继承，但是很有可能还是会在子元素中看到text-decoration的身影，应为父类的下划线*穿过*了子类，导致看起来子类有下划线一样**
**应用到父类的text-decoration，在子元素中是无法取消的**

## 文本渲染（text-rendering）
text-rendering的作用就是告诉浏览器加载字体时优先考虑什么
optimizespeed指优先考虑速度，optimizeLegibility值优先考虑清晰度,geometricProcision指尽最大可能保留字体原有样式
个人感觉作用不大，可以不看

## 文本阴影（text-shadow）
text-shadow专门用来给字体加阴影，适用于所有元素，不能继承
**text-shadow的语法为text-shadow:颜色,横向偏移长度值，纵向偏移长度值，模糊半径（可选）**
**正的长度值将阴影文本向右侧和下侧移动，所以负的长度值将阴影朝左侧和上侧移动**
第三个模糊半径的定义时：从阴影的轮廓到效果边界的距离。很怪，就像加了一个淡淡的背景

## 处理空白（white-space）
**适用于所有元素（css2.1），块级元素（css1和css2），没有继承性**
white-space有以下几个属性
 - normal(按照浏览器默认方式处理空白，即把空白压缩成一个空格）
 - nowrap（紧张元素中的文本换行，除非是br标签，同时压缩空白）
 - pre（空白不会被忽略）
 - pre-warp（保留空白，保留换行符，允许自动换行）
 - pre-line（压缩空白，保留换行符，允许自动换行）

## 设置制表符的宽度(tab-size)
**tab-size的初始值为8（一个制表符相当于8个空格，适用于所有块级元素，可以继承**
**注意，如果white-space的值导致空白被折叠了，那么tab-size就不再起作用（而且现在绝大部分浏览器不支持tab-size**

## 换行和段字
**hyphens用来自动断字，适用于所有元素，可以继承**
**如果hyphens的值为manual时，只有在文档中手动插入连字符&shy；等才可以断字，否则不断字。
如果是auto则浏览器自动判断。如果是none值时，即使手动插入连字符&shy；等都不能断字。每个浏览器使用这个值的方式不同，而且chrome不支持这个属性**

## word-break（软换行）
**word-break适用于所有元素，可以继承**
**word-break常用的几个值1，normal（按照正常的方式换行）2，break-all（在任何字符之间，即使是在一个英语单词内部）3，keep-all（在每个单词之间换行，不会在单词内部换行）**
**keep-all禁止在字符之间软换行即使一个字符一个词的CJK语言来说也是如此，因此，在中文等语言中，如果没有空格等符号就不会自动换行，即使会超过这个元素的宽度**

## line-break(CJK文字软换行）
**line-break主要应用于CJK文字和字符，如果一段文字中有英文和CJK文字，line-break只会应用到CJK文字中，不会应用到其他文字**
**line-break有这几个属性值，但我测试后感觉都差不多：
 1. auto
 2. loose
 3. normal
 4. strict

## 文本换行（overflow-wrap）
**overflow-wrap适用于所有元素，可以继承，它有两个值，normal和break-word；normal按照正常的方式换行，而break-word可以在单词内部换行**

**注意：只有white-space属性的值允许换行时，overflow-wrap才会起作用。如果white-space禁止换行，那么overflow-wrap没有任何作用**
**不要以为overflow-wrap：break-word和word-break：break-all效果一样，overflow-wrap仅当内容有溢出时才会起作用，如果源码中有空白，它也会换行。而word-break：break-all不同，它只在内容接触边界时换行，不管源码前面有没有空白**

## 书写模式（writing-mode)
**writing-mode适用于除表格外的所有元素，有继承性**
**writing-mode的默认值horizontal-tb的意思时行内方向为横向，块级方向为从上到下
vertical-rl（纵向从右到左），vertical-lr（纵向从左到右）

## 改变文本方向（text-orientation）
**text-orientation适用于出表格外的所有元素，可以继承**

## direction^[footnote text]
**direction适用于块级元素元素，可以继承**
**direction只有两个值ltr和rtl**

# 第七章视觉格式化基础
**默认情况下，内容区的背景会出现在padding的范围内，而margin区域始终是透明的，可以透过margin看到父元素。padding不允许有负数，而margin可以**
**border如果没有设置颜色值那么就与内容区的前景色相同，border不能为负数**

## 容纳块
容纳快是元素框体的“布局上下文”，容纳快一般由离元素最近的**列表项目**和**块级框**构成

## 调整元素的显示方式（display）
**display适用于所有元素，没有继承性**
**display改变的只是元素的显示方式，而不是元素本体，也就是说把块级元素生成的框变成行内框并不会把块级元素变成行内元素

## box-sizing
**box-sizing适用于能设置width和height的所有元素，没有继承性**
box-sizing属性能改变width和height的具体意义，如果设置值为border-box那么内容区到border总的宽度就等于你设置的width值，如果是默认值content-box时，width就是内容区的宽度

## 横向格式化（重点）
**横向格式化有7个值，margin-left,border-left,padding-left,width,padding-right,border-right,margin-right**
**其中只有width,margin-left,margin-right能设置为auto**
在width，margin-left，margin-right中，如果把一个设置为auto，那么那个auto就等于容纳块宽度-其他两个设置固定的值。
**如果把三个值都设置为一个固定的值，css术语来说就是过度约束，那么margin-right会被强制设置为auto，并且浏览器会欺骗你**

```css
div{
	width: 500px;

}
p{
	width: 100px;
	margin-left: 100px;
	/* margin-right: auto; //300px; */
}

div{
	width: 500px;
}
p{
	width: 100px;
	margin-left: 100px;
	/* margin-right: 100px; //被强制设置为300px,而且浏览器检查会欺骗你,看起来真的是100一样 */
}
```

如果把margin-left和margin-right都设置为auto，那么他们的值为(容纳块的width值-width值)/2
还可以把width值和一侧外边距设置auto，这时候那个外边距等于0

如果把三个值都设置为auto，那么两侧的外边距为0，而width等于容纳块的width值

**因为横向外边距不折叠，所以父元素的内边距，边框和外边距可能会影响子代**

## 负外边距
把外边距设置为负数，子元素比父元素宽了

## 置换元素
前面讲的应用于绝大多数，除了置换元素，在置换元素中，width：auto等于置换元素内容自身的宽度
**如果设定了height，而width为auto，那么宽度会随着高度按比例变化**

## 纵向格式化基础
**纵向格式化和横向格式化一样有7个值,margin-top,margin-bottom,border-top,border-bottom,padding-top,padding-bottom,height**
这7个值只有margin-top,height,margin-bottom可以设置为auto

**奇怪的是,在*常规流动模式下*如果把margin-top和margin-bottom设置为auto，两者自动计算为0（在弹性盒布局和定位就不一样了**

## 折叠纵向外边距
**纵向外边距有个很重要的特征，相邻的纵向*外边距*会折叠，只有外边距有这种折叠行为，内边距和边框都没有这种行为**

```css
li{
    margin-top: 10px;
    margin-bottom: 15px;
}
```
猜猜两个相邻的li距离是多少？25px?那你就错了！是15px！这是因为相邻的外边距在纵向上折叠了，换句话说**较小的外边距被较大的给消去了**

## 负外边距和折叠
如果两个相邻的外边距都是负值，浏览器则取绝对值较大的那个，**然后从正外边距中减去它的绝对值**也就是说，把负值和正值相加，得到的结果为两个元素之间的距离

## 列表项目
列表项目通常都有个记号，**但这个记号其实不在列表的内容区中**、

列表的标记可以放在内容区的外部，也可以作为行间内容，放在内容区的开头，**这取决于list-style-position属性的值**，如果把记号放在内部，列表项目和周围元素之间的关系就和块级元素一模一样

## 行内元素
**本节的内容均不适用于表格元素，表格元素和款级元素和行内元素有很大的差距**

## 行内格式化
line-height影响行内元素和其他行内内容，但不影响块级元素，块级元素可以设置line-height值，**但只对块级元素中的行内内容有视觉影响**

块级元素当然有line-height值，但是这个值将应用于块级元素内部的内容上（不管在不在行内元素中），相当于**块级元素中的各文本行就是行内元素**，不管是否真的在行内标签中都是如此。

## 行内非置换元素
**对于置换元素和匿名文本中，font-size值决定内容区的高度**
如果line-height与font-size的差是负数，那么内容区会比行内框小一点

# 第九章 颜色，背景和渐变

设置前景色最简单的方法就是设置color属性
背景色用background-color属性来声明
background-clip用于控制背景延伸到何处
背景定位用background-position属性来设置
background-origin
background-repeat背景重复方式（或者不重复）
背景粘附用background-attachment