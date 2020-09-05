## 选择器

### 简单选择器

- 元素选择器
- id选择器
- class选择器（**可以给一个元素设置多个class选择器，就像报了不同的班级**）
- 统配选择器（*）

### 复合选择器

- 交集选择器(选中同时复合多个条件的元素)
    - div.red(元素+类名/id名)
- 并集选择器(同时选择多个对应的元素)
    - .box1,.box2

### 关系选择器

- 父元素
- 子元素
- 祖先元素
- 后代元素
- 兄弟元素


- 子元素选择器(语法:父元素>子元素)
- 后代元素选择器(语法:祖先 后代)
- 兄弟元素选择器
    1. 选择后面第一个兄弟(第一个+第二个)
    2. 选择后面所有兄弟(第一个~第二个)

### 属性选择器

- 元素[属性名] 选择含有指定属性的元素
- 元素[属性名=属性值] 选择含有指定属性和属性值的元素
- 元素[属性名^=属性值] 选择属性值以指定值**开头**的元素
- 元素[属性名$=属性值] 选择以属性值**结尾**的元素
- 元素[属性名*=属性值] 选择属性值中含有某个值的元素

### 伪类选择器

- :first-child(选择第一个子元素)
- :last-child(选择最后一个子元素)
- :nth-child(选择第n个子元素)
    - 特殊值
    - n(选择第0到无穷个子元素)
    - 2n或even(选中偶数个子元素)
    - 2n+1或odd(选择奇数个子元素)
- :first-of-type(选择同类型的第一个元素)
- :last-of-type(选择同类型的最后一个元素)
- :nth-of-type(选择同类型的第n个元素)
- :not(将复合条件的元素从选择器中去除)

#### 超链接的伪类

- :link(没访问过的链接)(正常的链接)
- :visited(访问过的链接)(由于隐私原因,所以visited只能修改文字颜色)
- :hover(用来表示鼠标**移入**状态)
- :active(用来表示鼠标**点击**状态)

### 伪元素选择器

- ::first-letter(选择第一个字母)
- ::first-line(选择第一行)
- ::selection(选中时的样式)
- ::before(元素的开始位置[必须结合content使用])
- ::after(元素的结束位置[必须结合content使用])

### 继承

- 背景,布局这些样式都不会被继承
- 字体颜色可以被继承

### 权重

|选择器的权重   | 优先级 |
|    --------   | ----   |
| 内联选择器    | 1000   |
| id选择器      | 100    |
| 类和伪类选择器| 10     |
| 元素选择器    | 1      |
| 统配选择器    | 0      |
| 继承的样式    | 没有   |

比较优先级需要将所有的选择器相加进行计算(分组选择器单独计算)

**选择器的累加不会超过最大的数量集,类选择器不会超过id选择器(因为最高只能加到90不能加到一百多[其实可以,但这里只是为了方便理解],可以想一下CSS权威指南中的0,1,9,0.这样想就可以想通了)**

如果优先级相同,则使用最靠后的样式

**可以在某一个样式后面加入!important,则此时该样式会取到最高优先级,甚至超过内联样式**


## 像素百分比和常见的单位

### 长度单位
- 像素
- 百分比(相对于父元素的百分比,**可以跟随父元素的改变而改变**)
- em(em是根据font-size来计算的.1em=font-szie.**可以根据字体大小改变而改变**)
- rem(rem是相对于根元素(html)的font-size来计算的.1rem=font-size.)

### 颜色单位
1. 直接使用颜色名(blue,white,black)
2. 十六进制值.语法:#ABCDE(**如果颜色两位重复可以只写一个**)
3. **HSL值(H色相[0-360],S饱和度(浓度.0%-100%),L亮度(0%-100%)**
4. RGB值或RGBA.语法:RGB(红色,绿色,蓝色,**不透明度[1表示完全不透明,0表示完全透明]**)

## 布局(重点)

### 文档流
文档流:网页是一个多层的结构,一层叠加着一层.我们可以通过CSS来分别为每一层设置样式.作为用户来讲只能看到最顶上的一层.这些层中,最底下的一层称为文档流.我们所创建的元素默认在文档流创建

| 块元素                     |
| ---                        |
| 块元素在文档中独占一行     |
| 默认宽度是父元素的内容区   |
| 默认高度被子元素(内容)撑开 |
| 行内元素 |
| 行内元素不会独占一行(只占自身大小) |
| 行内元素在页面中从左向右排列,如果一行不能容纳所有行内元素,则元素会自动换到第二行 |
| 行内元素的默认宽度和高度都是被内容区撑开 |

### 盒子模型

每一个盒子都有以下几个部分:
1. 内容区(content)[元素中的所有子元素和文本内容]
2. 内边距(padding)[背景颜色会延申到内边距上][只能设置为正值]
3. 边框(border)
4. 外边距(margin)[不会影响盒子的大小,但会影响盒子的位置]

**内容区,内边距,边框组成了盒子的可见区域**

**重点:元素在页面中是自左向右排列,所以默认情况下margin-top,margin-left将会移动自身,但margin-right,margin-bottom则会移动其他元素**

**默认情况下盒子可见框的大小由内容区,内边框和边框决定(不包括margin,所以下面border-box也排除了margin)**
box-sizing用来设置盒子尺寸的计算方式(设置width和height的作用)
1. content-box(默认值,宽度和高度表示内容区的大小)
2. border-box(宽度和高度用来设置整个盒子的可见框的大小)

#### 盒子的水平布局(重点!)

元素在父元素中水平方向的位置由以下几个属性共同决定:
- margin-left
- border-left
- padding-left
- width
- padding-right
- border-right
- margin-right

一个元素在父元素中,**水平布局必须满足**以下等式

margin-left+border-left+padding-left+width+padding-right+border+right+margin+right = 父元素内容区的宽度

**如果这七个值加起来不等于父元素宽度,则称为过度约束,则会自动调整**

调整情况:
    1. 如果这七个值中没有为auto的,则浏览器会自动调整margin-right值让等式满足
    2. 这七个值中有一个auto(margin-left,width,margin-rigth),则自动设置那个auto值以使等式满足
    3. 这七个值中有两个auto[margin-left,width,margin-right]
        - 如果将一个宽度和一个外边距设置为auto,则会将宽度调整到最大
        - 如果margin-left和margin-right设置为auto,则两个平分多余空间]
    4. 如果三个值都是auto[margin-left,margin-right,width],则宽度能多大就多大

**如果子元素内容区宽度超过了父元素,则margin-right会自动调整为负数使其等式满足**


#### 盒子垂直方向布局

父元素的宽度默认被子元素撑开(**前提是不设置width或者设置width值为auto**)

如果设置了width值,但子元素高度超过了父元素.这就称为溢出.我们可以通过使用overflow来处理溢出的子元素

| overflow |
|---       |
| visible(默认值,子元素会从父元素中溢出,在父元素外部显示) |
| hidden(溢出的内容会被隐藏 |
| scroll(生成两个滚动条,通过滚动条来查看完整内容) |
| auto(根据需要生成滚动条,不会出现多余的滚动条 |

**如果想要单独在每个方向上设置可以使用overflow-x,overflow-y**

#### 垂直外边距的折叠

相邻的垂直方向外边距会发生重叠现象:
1. 兄弟元素
    - 兄弟元素两者之间取最大值[两者都是正数]
    - 如果一正一负则取两者的和[一正一负]
    - 如果相邻的都是负值,则取绝对值较大的[两个都是负数]
2. 父子元素
    - 父子元素相邻外边距,子元素会传递给父元素(上外边距)
    - 父子元素的折叠会引向到页面布局,必须要进行处理

#### 解决折叠问题(clearfix)
我们只需要在元素

#### 行内元素的盒模型

行内元素不支持设置高度和宽度,由内容撑开

行内元素可以设置padding,border,margin但垂直方向的padding,border,margin不会影响布局

| display |
| ---     |
| inline  |
| block   |
| inline-block |
| table   |
| none    |

| visibility |
| visible(默认值,元素在页面正常显示    |
| hidden元素在页面中不显示,但是位置会被占据 |





### 浮动

通过浮动可以使元素向父元素的左侧或右侧移动

**注意:元素设置为浮动后,水平布局的等式就不需要强制成立(宽度默认等于内容大小)**

元素设置浮动后,会完全从文档流中脱离,不再占用文档流的位置,所以元素下边的元素会自动向上移动

**浮动的特点**
1. 浮动的元素会完全脱离文档流,并不在占据文档中的位置
2. 设置浮动后元素回向父元素的左侧或右侧移动
3. 浮动元素默认不会从父元素中移出
4. 浮动元素向左或向右移动时,不会超过其他浮动元素
5. 如果浮动元素上边是一个没有浮动的块元素,则浮动元素无法上移
6. 浮动元素不会超过它上边的浮动元素的兄弟元素,最多就是和它一样高

**浮动可以很好的用来水平排列**

浮动元素不会盖住文字,以前发明浮动就是用来环绕文字的!

**脱离文档流特点(不是浮动特点)**
- 块元素
    1. 块元素不会独占一行
    2. 脱离文档流以后,块元素的高度和宽度默认被内容撑开
- 行内元素
    1. 行内元素脱离文档流以后会变成块元素,特点和块元素一样

**脱离文档流以后就不需要再区分块元素和行内元素了**

#### 高度塌陷问题

在浮动布局中,父元素的高度默认是被子元素撑开的,当子元素脱离文档流后将无法撑起父元素的高度,父元素高度塌陷以后其他的元素会自动上移,导致布局混乱.

处理方式:
**1.BFC(块级格式化环境)**
BFC是CSS中的一个隐藏的属性,可以为一个元素开启BFC.开启BFC后元素将会变成一个独立的布局.

**元素开启BFC的特点**
1. 开启BFC后的元素不会被浮动元素覆盖
2. 开启BFC的元素子元素和父元素外边距不会重叠
3. 开启BFC的元素可以包含浮动的元素

**可以通过以下方式来开启BFC**
1. 设置元素的浮动(不推荐,有副作用)
2. 将元素设置为行内块元素(不推荐,有副作用)
3. 将元素的overflow设置为一个非visible的值(推荐,值推荐使用auto)

**clear(清除浮动元素对当前元素的影响)**
可选值:
    - left(清除左侧浮动元素对当前元素的影响)
    - right(清除右侧浮动元素对当前元素的影响)
    - both(清除两侧中最大影响的那侧)

**撑起父元素高度源代码**
```html
		<style type="text/css">
			.box2{
				width: 200px;
				height: 200px;
				background-color: aqua;
				float: left;
			}
			
			.box1{
				border: 10px solid blue;
			}
			.box1::after{
				content: '';
				/* 默认是行内块元素所以需要转换 */
				display: block;
				clear: both;
			}
		</style>
	</head>
	<body>
		<div class="box1">
			<div class="box2"></div>
		</div>
		<script type="text/javascript" src="demo.js"></script>
	</body>
```

**clearfix**
通过试用clearfix也可以很有效的解决浮动的问题
```css
    .box1::after,.box1::before{
        content: '';
        display:table;
        clear:both;
    }
```
### 定位

#### 相对定位
- 当元素的position属性设置为relative时则开启了元素的相对定位
- 相对定位的特点
     1. 相对定位是参照于元素在文档流中的位置进行定位的
     2. 相对定位会提升元素的层级
     3. 相对定位不会使元素脱离文档流
     4. 相对定位不会改变元素的性质,块还是块,行还是行

#### 绝对定位
- 当元素的position属性设置为absolute时,则开启了绝对定位
- 绝对定位的特点
    1. 开启定位后,如果不设置偏移量元素的位置不会变化
    2. 开启绝对定位后,元素会从文档流中脱离
    3. 绝对定位会改变元素的性质,行内变成块,块的宽高被内容撑开
    4. 绝对定位会提升一个层级
    5. 绝对定位元素是基于包含块进行定位的

**包含块**
- 正常情况下:
    1. 包含块就是离当前元素最近的**块元素**
    ```html
        <div><div>div/><div>    <!-- 最外面的div是里面div的包含块 -->
        <div><span><em>hi<em/></span><div/> <!-- 最外面的div是em的包含块 -->
    ```
    2. 绝对定位的包含块:
        - 包含块就是离它最近的开启了定位的元素
        - 如果所有祖先都没有开启定位就根据html来定位

#### 固定定位
- 将元素的position设置为fixed则开启了元素的固定定位
- 固定定位也是一种绝对定位,所以固定定位的大部分特点都和绝对定位一样
- 唯一不同点是固定定位永远参考浏览器的视口进行定位
- 固定定位的元素不会随着网页的滚动条而滚动

#### 粘贴定位(当元素移动到某一处位置后就不会移动了[兼容性贼差!])

- 当元素的position属性设置为sticky时则开启了元素的粘贴定位
- 粘贴定位和相对定位的特点基本一致,不同的是粘贴定位到达某个位置后将其固定
    
#### 绝对定位元素的布局

水平布局需要满足以下等式:left + margin-left + border-left + padding+left + width + padding-right + margin-right + right = 父元素的宽度

当我们开启绝对定位以后,水平方向的布局就需要添加left和right两个值.此时规则和之前的一样只是多加了两个值.

如果发生过度约束,如果九个值中没有auto则自动调整right值让等式满足,如果有auto,则自动调整auto的值让等式满足

可以设置auto的值: margin width left right

因为left和right的默认值是auto,所以如果不知道left和right则等式不满足时,会自动调整这两个值

垂直布局的等式也要满足:top + margin-top + border-top + padding-top + height + padding-bottom + border-bottom + margin-bottom

#### 元素的层级

对于开启了定位的元素,可以通过z-index来指定元素的层级,层级越大越优先显示

**如果元素层级一样,则优先显示结构上靠下的元素**

**祖先元素的层级再高也不会盖住后代元素**


### 弹性盒(flex)

flex元素具有弹性,可以让元素随着网页大小的改变而改变

**主轴是弹性元素的排列方向称为主轴,与主轴垂直的方向称为垂轴**

**弹性容器**
要使用弹性盒，必须将一个元素设置为弹性容器(通过display:flex或者inline-flex来设置)

**弹性元素**
弹性容器的**直接子元素是弹性元素**
**弹性元素可以同时是弹性容器**


### 弹性容器的属性:
- flex-direction:

#### flex-direction 
flex-direction用来指定容器中弹性元素的排列方式,可选值有
- row:默认值,弹性元素在容器中水平排列(左到右) 主轴 至左向右
- row-reverse 弹性元素在容器中水平反方向排列(右向左) 主轴 自右向左
- column 弹性元素纵向排列(自上向下)
- column-reverse 弹性元素方向纵向排列(自下向上)


### 弹性元素的属性:
- flex-grow:指定弹性元素的伸展系数
- flex-shrink:指定弹性元素的收缩系数

## 默认样式

通常情况下,浏览器会为每个标签设置默认样式,他们会干扰我们的布局.所以我们需要reset.css 这是最佳方案,最差的方案就是*

## 轮廓阴影和圆角

outline:用来设置元素的轮廓线(和border不同的是轮廓不会引向到布局)
box-shadow:用来设置元素的阴影效果(阴影不会影响布局)

```css
    /* 第一个设置左侧阴影变量,第二个值设置下侧阴影变量,第三个值设置模糊半径,第四个值设置颜色 */
    box-shadow:10px 10px 50px black;
```

border-radius:用来设置圆角

```css
    /*
    border-top-left-radius:左上角
    border-top-right-radius:右上角
    border-bottom-left-radius:左下角
    border-bottom-right-radius:右下角 */
    border-radius:10px 10px 10px 10px;
```

## 字体

字体相关样式
    - color: 用来设置字体颜色
    - font-size: 用来设置字体大小
    - font-family: 用来设置字体族
    - font-family可以同时指定多个字体,它们分别用逗号隔开,字体优先使用第一个,如果没有第一个再去找第二个

**@font-face**

````html
    <style>
        @font-face{
            <!--字体的名称-->
            font-family:'lindaxia';
            <!--服务器中字体的路径-->
            src:"";
        }
    </style>
````

### 行高(line-height)
行高是指文字占据的实际高度,可以通过使用line-height来指定行高.行高可以指定一个大小(px,em),也可以设置一个整数.当设置一个整数时,行高将会是字体的指定的倍数.行高经常用来设置文字的行间距.

行高会在字体框的上下平均分配

**行间距=行高-字体大小**

### 字体简写属性

我们可以通过使用font来设置字体相关的所有属性

font基本格式要求:font-style font-variant font-weight font-stretch font-size/line-height font-family


**字体大小和字体祖是必须要写的,其他可选值font-style,font-variant,font-weight,line-height**

### 文本的水平对齐和垂直对齐
我们可以通过使用vertical-align设置元素的对齐方式
可选值:
    - baseline: 默认值,基线对齐
    - top: 顶部对齐
    - bottom: 底部对齐
    - middle: 居中对齐

**如果想更灵活的调整的话可以使用值来调整,正数朝上移动,负数朝下移动**

**如果图片底部出现一行空白那是因为img是替换元素,本质上和文本差不多,所以默认使用基线对齐.如果想消灭空白行则必须使用vertical-align**


### 其他文本样式

#### text-decoration 设置文本修饰
可选值:
    - none 什么都没有
    - underline 下划线
    - line-through 删除线
    - overline 上划线

```css
    text-decoration: underline blue dotted; //chrome,firfox都支持,ie不支持
```

#### white-space 设置网页如何处理空白
可选值:
    - normal 正常
    - nowrap 不换行
    - pre 保留空白

#### text-overflow 如何显示多余文本
```css
    text-overflow:clip //默认值
    text-overflow:ellipais //多余文本转换为省略号
```

#### iconFont

```html
    	<style type="text/css">
		i.iconfont{
			font-size: 50px;
		}
		.demo::before{  <!--第三种使用方法-->
			content: '\e664';
			font-family: 'iconfont';
			font-size: 100px;
		}
	</style>
    
    <body>
	<div>
		<i class="iconfont icon-arrow-right"></i> <!--第一种使用方法-->
		<p>This is class</p>
		<i class="iconfont">&#xe667;</i>    <!--第二种使用方法-->
		<p>This is 实体</p>
		<p class="demo"></p>
	</div>
</body>
````

## 背景

background-color:设置背景颜色

background-image:设置背景图片.如果背景图片小于元素,则图片自动平铺.如果背景图片过大,则一部分图片将无法显示

**我们可以同时设置背景图片和背景颜色**

background-repeat:用来设置背景方向重复方式.

background-position:用来设置图片的位置,通过top,left,right,bottom,center几个值来设置(注意!:**使用时必须要同时指定两个值,如果只写第一个则第二个默认就是center**)
    我们还可以通过水平偏移量来设置背景图片位置
    
background-clip:用来设置背景范围:
可选值:
    - border-box:默认值,背景会出现在边框的下边
    - padding-box:背景不会出现在边框,只会出现在内容区和内边距
    - content-box:背景只会出现在内容区

background-origin:背景图片偏移量的计算原点:
    - padding-box:默认值,background-position从内边距处开始计算
    - content-box:背景图片的偏移量从内容区处计算
    - border-box:背景图片从边框处开始计算

background-size:设置图片的尺寸

background-attachment:背景图片是否随着元素而移动
可选值:
    - scroll 默认值,背景图片会随着元素移动而移动
    - fixed背景图片会固定在页面中,不会随着元素移动

我们可以通过background来设置所有的背景属性,不过有几点需要注意:
    1. background-size必须写在background-position后面,并且试用/隔开.要想试用background-size就必须要设置background-position
    2. background-origin background-clip两个样式,origin必须要在clip前面

### 雪碧图

雪碧图的使用步骤
1. 先确定要使用的图标
2. 查看图标的大小
3. 根据测量结果创建一个元素
4. 将雪碧图设置为元素的背景
5. 设置一个偏移量以正确显示图片

### 渐变

渐变可以设置一些复杂的背景颜色,可以实现一个颜色向其他颜色过度的效果.

**渐变是图片,需要通过background-image来设置**

#### 线性渐变(linear-gradient)

线性渐变:颜色沿着一条直线发生变化

我们还可以设置渐变的方向
- to left
- to right
- to bottom 
- to top
- deg deg表示度数
- turn 表示圈

```css
linear-gradient(red,yellow); //红色在开头,黄色在结尾,中间是过度颜色
linear-gradient(to left, red,yellow); // 渐变从左边开始
linear-gradient(red 50px,yellow 100px);  //红色从50像素后开始渐变,黄色从100像素位置后开始渐变
repeating-linear-gradient(red,yellow); // 重复渐变
```

#### 径向渐变(radial-gradient)

默认情况下径向渐变会根据元素的形状来计算.正方形 -> 圆形,长方形 -> 椭圆形

我们也可以通过使用circle,ellipse来设置形状

radial-gradient默认语法:radial-gradient(大小 at 位置,颜色 位置,颜色 位置);

大小有几个可选值:
- circle 圆形
- ellipse 椭圆形
- closest-side 近边
- closet-corner 远边
- farthest-corner 远角

位置有几个可选值:top,right,left,bottom,center或者精确数值


## 表格

在table标签中tr标签表示一行,td标签表示一个单元格

**如果想让一个单元格横着占据两个单元格或者以上的位置可以使用colspan,如果想纵向占据两个单元格或者以上的位置可以使用rowspan来设置**

### 长表格

我们可以将表格分为三个部分
- 头部 thead
- 主体 tbody
- 腿部 tfoot

它们三个分别表示三个标签,其中头部还有一个特殊标签th,这个标签可以代替td.专门用于thead里

### 表格的样式

border-spacing:可以用来设置table边框和td边框的距离

border-collapse:可以用来设置边框是否合并

**如果表格中没有使用tbody而是直接使用tr,那么浏览器会自动创建一个tbody,并将tr全部放到tbody中,所以tr不是table的子元素!tr不是table的子元素!tr不是table的子元素!**

默认情况下元素在表格中是垂直居中的,我们可以通过vertical-align来设置

## 表单
**表单用于将数据提交给服务器**

input的type属性值:
- text:文本框
- password:密码框
- submit:提交按钮
- radio:单选按钮
- checkbox:多选按钮
- button:按钮
- reset:重置按钮
- color:调色板
- email:文本框(但会自动检查是否是邮箱格式)

**如果想关闭文本自动补全功能可以使用autocomplite="off"**

如果想让表单项只读可以使用readonly,只读的表单项会提交

如果想禁用表单项可以使用disable禁用的表单项不会提交

autofocus可以用来自动获取焦点

**单选框,多选框都必须要指定一个value值,因为数据在提交时是提交的选中的元素的value值,我们可以通过checked来使选择框默认选中.**

**如果想让一群单选框,多选框联系起来则要使用相同的name值**

### 下拉选项
```html
    <select name="hello">
        <option value='1'>选项一</option>
        <option selected value='2'>选项二</option> <!-- 我们可以通过使用selected来使下拉框默认选中 -->
        <option value='3'>选项三</option>
    </select>
```

## 过渡

通过过渡(transition)可以指定一个元素变换时的切换方式

transition-property:指定要执行过度的属性,多个属性可以使用'逗号'隔开.如果所有属性都需要过度则使用all关键词.
大部分属性都支持过度,注意过渡时必须从一个有效值向另一个有效值进行过渡
  
transition-duration:用于指定过渡效果持续的时间

transition-timing-function:用于指定动画执行的方式
可选值:
    - ease:默认值,慢速开始,先加速,再减速
    - linear:匀速移动
    - ease-in:加速运动
    - ease-out:减速运动
    - ease-in-out:先加速,后减速
    - cublic-bezier()需要时可以去网上差看
    - step():分步数执行过渡元素
    1. 可选值
    2. end:在时间结束时执行(默认值)
    3. start:在时间开始时执行过渡元素

transition-delay:过渡效果的延迟,等待时间一段时间后在执行过渡

**transition:简写属性,只有一个要求,如果要写延迟,则两个时间中第一个是持续时间,第二个时间是延迟时间**

## 动画

动画和过渡类似,都可以实现一些动态的效果.不同的是过渡只能在某个属性发生改变时触发,而动画可以自动触发

设置一个动画效果,必须要设置一个关键帧
```css
<!--name表示动画的名字-->
@keyframes name{
<!--from表示动画开始 也可以用0%-->
			from{
			
			}
<!--to动画结束,也可以使用100%-->
			to{
			
			}
		}
```

 animation-name:要对当前元素生效的关键帧的名字
 animation-duration:动画执行的时间
 animation-delay:动画的延时
 animation-iteration-count:动画执行的次数(可选值:infinite 无限执行)
 animation-direction:动画运行的方向
 
 可选值
  - normal: 默认值,从from到to,每次都这样执行
  - reverse: 从to向from运行,每次都这样
  - alternate:从from向to运行,重复执行动画时反向执行
  - alternate-reverse:从to向from运行,重复执行动画时反向执行

animation-play-state:设定动画的执行状态(可选值:running[默认值,动画执行],paused[动画暂停])

animation-fill-mode:动画的填充模式:
可选值:
 - none:默认值,动画执行完毕后回到原来的位置
 - forwards:动画执行完毕元素会停止在动画结束位置
 - backwards:动画延时等待时,元素就会处在开始位置
 - both:结合了forwards和backwards


## 变形

变形是用来通过CSS来改变元素的形状或位置

**变形不会影响到页面布局**

transform:用来设置元素的变形效果
- 平移
- translateX() 沿着X轴方向平移
- translateY() 沿着Y轴方向平移
- translateZ() 沿着Z轴方向平移

**通过rotate可以使元素沿着x,y或z旋转指定的角度**
- rotateX()
- rotateY()
- rotateZ()

是否显示元素背面我们可以通过使用backface-visibility来设置

设置视距可以通过perspective来设置

**通过scale可以产生放大或缩小的效果**
- scaleX():水平方向缩放
- scaleY():垂直方向缩放
- scale():双方向缩放

## less

在原生css中支持变量设置和简单计算

- --*变量设置
- calc():简单计算

**但是它们兼容性很差,所以不要使用它们**

```less
    body{
    // 在less中对body的后代元素设置
        div{
        
        }
        // 对body中的子元素设置
        > div{
        
        {
    }
```

在less中单行注释使用//,多行注释使用/**/

**在less中变量使用@符号定义**

```less
@a:130px;
@b:box6;
    div{
        //直接使用则以 @变量名 的方式使用
        width:@a;
    }
    //作为类名,或者一部分使用时则必须以 @[变量名] 的形式来使用
    .@[b]{
    
    }
```

**&符号就表示外层子元素**
```less
.box{
    &:hover{
    
    }
    .son{
        &:hover{}
    }
}
```

编译后:
```css
    .box{}
    .box:hover{}
    .box .son{}
    .box .son:hover{}
```

### mixin(混合)

编译前:
```less
*{
	margin: 0;
	padding: 0;
}
.box1{
	width: 200px;
	height: 200px;
}

//通过扩展使box2拥有颜色
.bo2:extend(.box1){
	background-color: #bfa;
}

.box3{
	width: 20px;
	height: 20px;
}

//通过混合让box4拥有颜色,但box3也会出现在css里面
.box4{
	.box3();
	background-color: #bfa;
}

//专门定义一个混合来使他人使用,box5不会出现在css里面
.box5(){
	width: 20px;
	height: 20px;
}
.box6{
	.box5();
	background-color: #bfa;
}
```

编译后:
```css
* {
  margin: 0;
  padding: 0;
}
/*通过扩展使得代码更加简洁*/
.box1,
.bo2 {
  width: 200px;
  height: 200px;
}
.bo2 {
  background-color: #bfa;
}
/*混合会出现在代码里*/
.box3 {
  width: 20px;
  height: 20px;
}
.box4 {
  width: 20px;
  height: 20px;
  background-color: #bfa;
}
/*定义专门的混合box5,所以不会出现在混合里*/
.box6 {
  width: 20px;
  height: 20px;
  background-color: #bfa;
}
```

### 混合函数

```less
*{
	margin: 0;
	padding: 0;
}
//通过给混合设置参数实现类似方法的效果
.box1(@w,@h){
	width: @w;
	height: @h;
}
.box2{
	.box1(100px,200px);
}
//给混合函数设置默认值
.box3(@w:100px,@h:200px,@color:red){
	width: @w;
	height: @h;
	color: @color;
}
.box4{
	.box3(@color:blue);
}
```

编译后:
```css
* {
  margin: 0;
  padding: 0;
}
.box2 {
  width: 100px;
  height: 200px;
}
.box4 {
  width: 100px;
  height: 200px;
  color: blue;
}
```

### 导入

```less
//导入通过@import方法
@import 'demo.less';
*{
	margin: 0;
	padding: 0;
}
.box1{
	width: @w;
	height: @h;
}
```

## 像素
像素:
: 屏幕是由一个一个的小点构成
: 分辨率: 1920 * 1000 就是小点的数量
: 在前端开发中像素分为两种情况
- 物理像素
: 上述所说的小点就是物理像素
- css像素
: 编写网页时我们所说的像素


一个css像素最终由几个物理像素显示,默认由浏览器决定.**默认情况**下在pc端:一个css像素 = 一个物理像素

视口:
: 视口就是屏幕中用来显示网页的区域
: 可以通过查看视口的大小,来观察css像素和物理像素的比值
> 默认情况下:
> 视口宽度 1920px(css像素)  1920(物理像素)  此时css像素和物理像素比是1:1

***

> 放大两倍后
> 视口宽度960px(CSS像素)    1920(物理像素)  此时css像素和物理像素之比是1:2

<p style="text-decoration: underline; color: red;">我们可以通过改变视口的大小,来改变css像素和物理像素的比值</p>

### 完美视口

在不同的屏幕,单位像素的大小是不同的,像素越小越清晰.

> 24寸 1920px*1000px
> 苹果6 750px*1334px
>从中可以看出智能手机的像素点远远小于计算机像素点

那么一个900px的网页在手机中如何显示呢?

>默认情况下,**移动端网页都会将视口设置为980像素**(css像素),以确保pc端网页可以在移动端正常访问.但是如果网页的宽度超过了980像素移动端的浏览器会**自动对网页进行缩放以完整显示网页**

移动端视口默认大小是980px(css像素)
> 默认情况下,移动端的像素就是 980/移动端宽度 (980/750)
> 如果我们直接在网页中编写移动端的代码,这样在980的视口下,像素比是非常不好的,会导致网页中的内容非常非常的小
> 缩写页面时,必须要有一个合理像素比 1css像素对应两个物理像素 或者 1css像素对应3个物理像素
> 我们可以通过meta标签来设置视口大小

将网页设置为完美视口的代码

```css
<meta name='viewport' content='width=device-width, initial-scale=1.0'>
```

不同设备的完美视口是不一样的.由于完美视口不同.所以 375 在不同设备情况下是不同的.

==**所以在移动端开发,就不能使用px这个单位了**==


### VW代表视口的宽度
- 100vw = 一个视口的宽度
- 1vw = 1%视口的宽度

**vw这个单位永远相当于视口的宽度进行计算**

*[375]:(iphone4完美视口)

在网页中字体最小是12px,不能设置一个比12px还小的字体.如果我们设了一个小于12px的字体,则自动设置为12px

