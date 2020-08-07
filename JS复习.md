# 操作符
**在js中永远不要测试两个小数的运算，连最简单的0.1＋0.2都可以等于0.3000000004你还相信js的小数运算吗？** 
**Nan和谁都不相同，包括Nan本身**  

Number()转换规则如下
	1. 如果字符串只包含数字(包括前面有正或负号的情况下),则将其转换为十进制数字
	2. 如果字符串中包含有效的小数格式，则将其自动转换为对应的小数
	3. 如果字符串中包含有效的16进制格式，则将其转换为16进制
	4. **如果字符串包含除以上格式外的字符串,则将其转换为NaN**
	5. 如果是对象，则调用对象的valueof方法，让后依据前面的转换，如果转换值是Nan，则再次调用toStirng方法再尝试

parseInt()转换规则如下:
	1. 如果第一个字符是数字，则会继续解析第二个字符，直到解析到不是数字的字符
	2. 如果第一个字符不是数字或正负号，则将其转换为NaN

除了null和undefined其他的基本类型都有toString方法
在不知道转换对象是否是null或者undefined时可以使用String方法，规则如下
	1. 如果对象有toString方法则调用该方法
	2. 如果对象是null则返回null
	3. 如果对象是undefined则返回undefined

**按位异或(我的最差的点)**
|  第一个数值的位   | 第二个数值的位    | 结果    |
| --- | --- | --- |
|  1   | 1   | 0    |
| 1    | 0    | 1    |
| 0    | 1    | 1    |
| 0    | 0    | 0    |

**逻辑非**
逻辑非用!表示，应用到不同的值有不同的表现
	1. 如果操作数是一个对象，返回false
	2. 如果操作数是一个空字符串，则返回true
	3. 如果操作数是一个非空字符串，则返回false
	4. 如果操作数是数值0，则返回true
	5. 如果操作数是任意非0数字，则返回false
	6. 如果操作数是null，则返回true
	7. 如果操作数是NaN，则返回true
	8. 如果操作数是undefined，则返回true

**逻辑与**
	1. 如果第一个操作数是对象，则返回第二个操作数
	2. 如果第二个操作数是对象，则只有在第一个操作数的求值结果为true的情况下才会返回该对象
	3. 如果两个操作数都是对象，则返回第二个操作数
	4. 如果有一个操作数是null，则返回null
	5. 如果有一个操作数是NaN,则返回NaN
	6. 如果有一个操作数是undefined，则返回undefined

**逻辑或**
	1. 如果第一个操作数是对象，则返回第一个操作数
	2. 如果第一个操作数的求值结果为false，则返回第二个操作数
	3. 如果两个操作数都是对象，则返回第一个操作数
	4. 如果两个操作数都是null，则返回null
	5. 如果两个操作数都是NaN，则返回NaN
	6. 如果两个操作数都是undefined，则返回undefined

**关系操作符**
	1. 如果两个操作数都是数值，则执行数值比较
	2. 如果两个操作数都是字符串，则比较两个字符串对应的字符编码值
	3. 如果一个一个操作数是数值，则将另一个操作数转换为一个数值，然后执行数值比较
	4. 如果一个操作数是boolean，则将其转换为数值进行比较

**相等比较==**
```javascript
//在==的比较中null和undefined是等价的
//全等===来定义，==只是单纯比较数值是否一样，===则比较数值和类型是否相同
```
**理解参数**
在JavaScript函数中不介意你传入多少个参数，也不关心类型是什么。之所以会这样，是因为**JavaScript中的参数是由一个数组表示，在函数体内可以通过arguments来访问数组的成员**

**在JavaScript中没有重载,但是我们可以通过传入不同的参数类型和数量进行判断并作出不同的反应**
```javascript
function doAdd(){
	if(arguments.length == 1){
		alert(arguments[0] + 10);
	}else if(arguments.length == 2){
		alert(arguments[0] + arguments[1] );
   }
}
//调用
doAdd(10);//20
doAdd(10,20);//30
```

# 变量，作用域和内存问题
在JS中包含两种不同数据类型的值：基本类型和引用类型  
基本类型指的是简单的数据段，而引用类型值指的是那些可能由多个值构成的对象

**在很多语言中，字符串以对象的形式来表示，因此被认为是引用类型的，JS抛弃了这一个传统**
复制基本类型就真的是复制基本类型的值，而复制对象的话就是复制指针了

检测基本数据类型用typeof是一个好方法，但是检测引用类型就不太行了，因为null和一个真正的对象它分不清，都会返回Object，这时候就需要使用instanceof来进行判断

# 引用类型
创建Object的两种方式
```javascript
//第一种
var person = new Object();
	person.name = "lindaxia";
	person.age = 20;
//第二种,首选第二种
var person = {
	name : "lindaxia",
	age : 20
};
```

## Array类型
在JS中数组可以保存任何类型的数据类型，也就是说第一个可以是int，第二个可以是String，第三个也可以是Object
```javascript
//创建数组的两种方法
//第一种
var colors = new Array();
//如果知道数组的大小，就可以用这种方式
var color = new Array(1);
//第二种
var colorss = ['red','blue','green'];
```
**在JS中，数组的length方法不仅仅只能读取，还可以修改，我们可以通过修改lenght的值来增加或删除数组中的元素**

在JS中提供了两个方法来实习类似栈的行为(栈是一种后进先出的顺序结构)
	1. push()方法可以接受任意数量的参数，把他们添加到数组末尾，并返回修改后的数组长度
	2. pop()方法可以移除数组末尾最后一项，并返回最后一项的值

在JS中提供了shift()方法来实现类似队列的行为(队列是一种先进先出的顺序结构)
**shift()方法可以移除数组中的第一项并返回改项**
**在JS提供了unshift()方法来向前端添加任意项目并返回新的数组长度**
**在JS中提供了reverse()【反转数组】和sort()【从小到大重新排列数组】**
concat方法用于向数组末尾添加参数，slice方法能够基于一个或多个项目创建一个新的数组
**splice方法是最强大的数组方法了，它用于向数组中部插入项，使用这种方法的方式有如下三种**
	1. 删除：可以删除任意数量的项，只需指定两个参数：要删除的第一项位置和要删除的例如splice(0,2)会删除数组的前面两项
	2. 插入：可以向指定位置插入任意数量的项目，只需要提供三个参数：起始位置，0（要删除的项数），要插入的项，如果要插入多个项，可以再传入第4，5，6个项.例如:splice(2,0,'red','green')会从数组的第3项开始插入数据
	3. 替换：可以向指定位置插入任意数量的项，同时删除任意数量例如：splice(2,1,'red','green')会删除第三个项，并添加数据
**splice方法始终都会返回一个数组**

**位置方法**
在JS中提供了indexof和lastindexof两个方法用于接收参数，并返回该点的值。其中indexof是从前向后，而lastindexof是从后到前,如果没有找到该字符串则返回-1.这两个方法都会接受第二个参数，表示从字符串的哪个位置开始搜索

**数组迭代**
在JS中提供了5个迭代方法
	1. every：对数组中每一项运行给定的值，如果该函数对每一项都返回true，则返回
	2. filter：对数组中每一项运行给定函数，返回该函数会返回true的项组成的数组
	3. foreach：对数组中的每一项运行给定的函数，这个方法没有返回值
	4. map：对数组中每一项运行给定的函数，返回每次函数调用的结果组成的数组
	5. some：对数组中每一项进行给定的函数，如果该函数对任意一项返回true，则返回true
	6. **以上方法都不会修改数组中的值**


## Date类型

## RegExp类型
在JS中可以通过以下语法创建一个正则表达式
```javascript
	//第一种创建方式
	var expression = /pattern/flags;
	//第二种创建方式
	var pattern2 = new RegExp("[bc]at","i");
```
其中flags表示匹配模式，JS支持三种匹配模式
	1. g:表示全局模式，即匹配模式将被应用到所有字符串，而并非在发现第一个匹配项时立刻停止
	2. i：表示不区分大小写模式
	3. m：表示多行模式，即在一行文本末尾时还会继续查找下一行是否存在与模式匹配的项

正则表达式提供了两个方法exec和test方法。test方法接受一个字符串，如果能与正则表达式匹配就返回true否则返回false

## function类型
**使用不带园括号的是访问函数名指针，而非调用函数**
在函数内部有两个特殊的对象：arguments和this。arguments主要是保存函数的参数，而this指向的是引用函数以执行的环境对象

## 基本包装类型
JS提供了三个基本包装类Boolean，Number，String  
使用Boolean对象会有各种各样的“bug”，所以建议永远不要使用Boolean包装类(Number也是一样)
String对象都有lenght，charat和charcodeat方法。其中length会返回字符串中包含多少字符。charat方法会返回给定位置的那个字符，而如果你想得到字符编码就只能使用charcodeat了。

字符串还有一个拼接方法concat

JS还提供了三个基于子字符串创建新字符串的方法：slice，substr和substring。
它们都可以接受一个或者两个参数。其中第一个参数指定开始的位置，而第二个参数slice和substring指定的是子字符串最后一个字符的位置，而substr第二给参数指定的是返回的字符数
```javascript
	var str = "0123456789ABC";
	console.log(str.slice(3));
	console.log(str.substr(3));
	console.log(str.substring(3));
	console.log(str.slice(3,5));
	console.log(str.substr(3,5));
	console.log(str.substring(3,5));
	// output:
	// 	3456789ABC
	// 	3456789ABC
	// 	3456789ABC
	// 34
	// 34567
	// 34
```
**然而如果是负数结果就不相同了。其中slice方法会将传入的负值与字符串长度相加，substr会将负值的第一个参数加上字符串的长度，而将第二个参数转换为0.最后substring方法会将所有的负数参数都转换为0**

```javascript
var str = "0123456789ABC";
	console.log(str.slice(-3));
	console.log(str.substr(-3));
	console.log(str.substring(-3));
	console.log(str.slice(3,-5));
	console.log(str.substr(3,-5));
	console.log(str.substring(3,-5));
	// output:
	// 	ABC
	// 	ABC
	// 	0123456789ABC
	// 	34567
	// 	空字符串
	// 	012
```

字符串提供了大小写转换的方法toLowerCase，toUpperCase

**JS中最强大也最危险的方法eval**
eval方法会接受一个参数，那个参数就是要执行的JS代码
```javascript
//这段代码等于alert("hi");
eval("alert('hi')");
```
## Math对象
Math有max方法，ceil向上取整，floor向下取整，round四舍五入，random取随机数

# 函数表达式
在JS中定义函数有两种方法:1是函数声明，2是函数表达式
```javascript
sayHi();
//函数声明创建函数，这里利用了函数声明提升。函数声明提升意味着可以把函数调用放在它的创建语句前面
function sayHi(){
	alert("hi");
}
//函数表达式创建函数
var sayHiTwo = function(){
	alert("HIHI");
}
```

## 闭包
匿名函数和闭包的区别是：**闭包可以访问另一个函数作用域中的变量**

# BOM
**抛开全局变量会成为window对象的属性不谈，定义全局变量与在window对象上直接定义属性还是有一点差别：全局变量不能通过delete操作符删除，而直接在window对象上定义的属性可以**
**还有一点就是尝试访问未声明的变量会抛出异常，但是通过查询window对象，可以知道某个可能未声明的变量是否存在。（如果未声明会显示undefined，而不会抛出异常)**

在window中,outerWidth,outerHeight分别保存着浏览器本身的尺寸,而innerWidth,innerHeight分别保存着视口的尺寸

可以通过window.open()方法打开新网页,它可以接受四个参数(URL,目标窗口,一个特性字符串,以及一个新页面是否取代浏览器历史记录当前页面加载的布尔值)
```javascript
window.open("http://www.baidu.com","_blank","height=100,width=100");
```
可以通过window.close()关闭弹出的窗口,但只能关闭弹出的窗口,最开始的窗口只能用户自己关闭.但经过我的测试,好像chrome可以关闭

我们可以通过以下方法来检测浏览器是否自动拦截了弹窗
```javascript
var open = window.open("http://www.baidu.com","_blank","height=100,width=100");
if(open == null){
	console.warn("浏览器禁止打开网站!");
};
```
超时调用是setTimeout,间歇调用是setInterval()
**最好不要使用间歇调用**
调用setTImeout()之后,该方法会返回一个数值ID,表示超时调用,这个超时调用ID是计划执行代码的唯一标识符,可以通过ID来取消超时调用
```JavaScript
//设置超时调用
var timeoutid = setTImeout(function(){alert("hi"),1000);
clearTimeout(timeoutid);
```

## 最有用的BOM对象-location

## 我觉得也挺厉害的BOM对象-navigator

## 系统对话框
alert()警告框，confirm()确认,取消框,prompt()输入框
如果用户点击了ok,confirm会返回true,如果用户点击了取消或者关闭了就会返回false
如果用户点击了输入框的ok,就会返回输入的值(即便他什么也没有输),如果用户点击了取消或者关闭就会返回null

# 客户端检查
**不到万不得已,就不要使用客户端检测,只要能找到更加通用的方法,就该使用更通用的方法**

# DOM
文档元素是最外层的元素,在html中文档元素始终都是<html>标签

getAttribute()增加特性，removeAttribute()删除特性,setAttribute()设置特性