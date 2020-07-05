##字符串方法及解释
capitalize()把字符串的第一个字符改为大写  
casefold()把整个字符串的所有字符改为小写  
center(width)将字符串居中，并使用空格填充至长度 width 的新字符串  
count(sub[, start[, end]])返回 sub 在字符串里边出现的次数，start 和 end 参数表示范围，可选。  
encode(encoding='utf-8', errors='strict')以 encoding 指定的编码格式对字符串进行编码。
endswith(sub[, start[, end]])检查字符串是否以 sub 子字符串结束，如果是返回 True，否则返回 False。start 和 end 参数表示范围，可选。  
expandtabs([tabsize=8])把字符串中的 tab 符号（\t）转换为空格，如不指定参数，默认的空格数是 tabsize=8。  
find(sub[, start[, end]])检测 sub 是否包含在字符串中，如果有则返回索引值，否则返回 -1，start 和 end 参数表示范围，可选  。
index(sub[, start[, end]])跟 find 方法一样，不过如果 sub 不在 string 中会产生一个异常。  
isalnum()如果字符串至少有一个字符并且所有字符都是字母或数字则返回 True，否则返回 False。  
isalpha()如果字符串至少有一个字符并且所有字符都是字母则返回 True，否则返回 False。  
isdecimal()如果字符串只包含十进制数字则返回 True，否则返回 False。  
isdigit()如果字符串只包含数字则返回 True，否则返回 False。  
islower()如果字符串中至少包含一个区分大小写的字符，并且这些字符都是小写，则返回 True，否则返回 False。  
isnumeric()如果字符串中只包含数字字符，则返回 True，否则返回 False。  
isspace()如果字符串中只包含空格，则返回 True，否则返回 False。  
istitle()如果字符串是标题化（所有的单词都是以大写开始，其余字母均小写），则返回 True，否则返回 False。  
isupper()如果字符串中至少包含一个区分大小写的字符，并且这些字符都是大写，则返回 True，否则返回 False。  
join(sub)以字符串作为分隔符，插入到 sub 中所有的字符之间。  
ljust(width)返回一个左对齐的字符串，并使用空格填充至长度为 width 的新字符串。  
lower()转换字符串中所有大写字符为小写。  
lstrip()去掉字符串左边的所有空格  
partition(sub)找到子字符串 sub，把字符串分成一个 3 元组 (pre_sub, sub, fol_sub)，如果字符串中不包含 sub 则返回 ('原字符串', '', '')  
replace(old, new[, count])把字符串中的 old 子字符串替换成 new 子字符串，如果 count 指定，则替换不超过 count 次。  
rfind(sub[, start[, end]])类似于 find() 方法，不过是从右边开始查找。  
rindex(sub[, start[, end]])类似于 index() 方法，不过是从右边开始。  
rjust(width)返回一个右对齐的字符串，并使用空格填充至长度为 width 的新字符串。  
rpartition(sub)类似于 partition() 方法，不过是从右边开始查找。  
rstrip()删除字符串末尾的空格。  
split(sep=None, maxsplit=-1)不带参数默认是以空格为分隔符切片字符串，如果 maxsplit 参数有设置，则仅分隔 maxsplit 个子字符串，返回切片后的子字符串拼接的列表。  
splitlines(([keepends]))在输出结果里是否去掉换行符，默认为 False，不包含换行符；如果为 True，则保留换行符。。  
startswith(prefix[, start[, end]])检查字符串是否以 prefix 开头，是则返回 True，否则返回 False。start 和 end 参数可以指定范围检查，可选。  
strip([chars])删除字符串前边和后边所有的空格，chars 参数可以定制删除的字符，可选。  
swapcase()翻转字符串中的大小写。  
title()返回标题化（所有的单词都是以大写开始，其余字母均小写）的字符串。  
translate(table)根据 table 的规则（可以由 str.maketrans('a', 'b') 定制）转换字符串中的字符。   
upper()转换字符串中的所有小写字符为大写。  
zfill(width)返回长度为 width 的字符串，原字符串右对齐，前边用 0 填充。  

***
python一行书写多个语句用;隔开  
取得一个变量的类型，用type()或者isinstance()  
python可以用//来实现类似于java/的效果，but3.0//2.0等于1.0  
5**-2等于1/25  
assert关键字可以称为断言，但这样关键字后面为假时，程序自动崩溃并报错  
x,y=y,x可将两个的值快速交换  
成员资格运算符，in，用于检查一个值是否在序列中，是返回True，否则返回False  
range(10)生成[0,1,2,3,4,5,6,7,8,9]不包含10  
在数组中添加元素可以用append，insert，和extend方法，其中append只能添加一个元素，insert用于在某个地方插入某个元素，extend用于插入多个元素  
member.append(['a','b'])的意思是插入一个数组，而member.extend(['a','b'])的意思是插入两个元素  
三引号字符串在不赋值的情况下，通常当做跨行注释使用  
str[::3]意思是从左到右，间隔为三取字符  
函数文档可以用help来访问，这是#不能的  
如果希望在函数中修改全局变量的值，应该使用blobal关键字，如果不用关键字的话就会创建一个名字一样的局部变量来屏蔽修改    
在嵌套函数中，如果希望在函数内部修改外部函数的局部变量，应该使用nonlocal关键字

汉诺塔代码

    def hanoi(n,x,y,z):
    if n == 1:
        print(x,'-->',z)
    else:
        hanoi(n-1,x,z,y)
        print(x,'-->',z)
        hanoi(n-1,y,x,z)

    n = int(input('please enter your number'))
    hanoi(n,'X',"Y",'Z')
***
兔子问题代码

        def fab(n):
        n1 = 1
        n2 = 1
        n3 = 1
        if n<1:
            print('error')
            return -1
        while(n-2)>0:
            n3 = n2 + n1
            n1 = n2
            n2 = n3
            n -= 1
        return n3
    result = fab(4)
    if result != -1:
        print(result)
***

    def Fun(n):
     if n <1:
         print('error')
         return -1
     if n == 1 or n == 2:
         return 1
     else:
         return Fun(n-1) + Fun(n-2)
***
##文件打开模式
|'r'|以只读方式打开文件|
|:---:|:---:|
|'w'|以写入的方式打开文件，会覆盖已存在的文件|
|‘x’|如果文件已经存在，使用此模式打开将引发异常|
|‘a’|以写入模式打开，如果文件已经存在，则在末尾追加写入|
|‘b’|以二进制模式打开文件|
|‘t’|以文本模式打开（默认）|
|‘+’|可读写模式(可添加到其他模式中使用)|
|‘u’|通用换行符支持|
##文件对象方法
|文件对象方法|执行操作|
|:---:|:---:|
|f.close|关闭文件|
|f.read([size=-1])|从文件读取size个字符，当未给定size或给定负数的时候，读取剩余的所有字符，然后作为字符串返回
|f.readline([size=-1])|从文件读取并返回一行（包括行结束符），如果有size有定义则返回size个字符|
|f.write(str)|将字符串str写入文件|
|f.writelines(seq)|向文件写入字符串序列seq，seq应该是一个返回字符串的可迭代对象|
|f.seek(offset, from)|在文件中移动文件指针，从from（0代表文件起始位置，1代表当前位置，2代表文件末尾）偏移offset个字节
|f.tell()|返回当前在文件中的位置|
|f.truncate([size=file.tell()])|截取文件知道size个字节，默认是截取到文件指针当前位置

##os模块中关于文件/目录常用的函数使用方法
|函数名|使用方法|
|:---:|:---:|
|getcwd()|返回当前工作目录|
|chdir（path）|改变工作目录|
|listdir（path=‘.’）|列举指定目录中的文件名（‘.’表示当前目录，‘..’表示上一级目录）|
|mkdir（path）|创建单层目录，如果目录已经存在则抛出异常|
|makedirs(path)|递归创建多层目录，如该目录已经存在抛出异常，注意：‘E：\\a\\b’和'E:\\a\\c'并不会冲突|
|remove（path）|删除文件|
|rmdir（path）|如该目录非空则抛出异常|
|removedirs（path）|递归删除目录，从子目录到父目录逐层尝试删除，遇到目录非空则抛出异常|
|rename（old，new）|将文件old重命名为new|
|system（command）|运行系统的shell命令|
|walk（top）|遍历top路径以下的所有子目录，返回一个三元组：（路径，【包含目录】，【包含文件】）【具体实现方案请看第30课后作业】|
|以下是支持路径操作中常用到的一些定义，支持所有平台||
|os.curdir|指代当前目录（'.'）|
|os.pardir|指代上一级目录（'..'）|
|os.sep|输出操作系统特定的路径分隔符（Win下为'\\'，Linux下为'/'）|
|os.linesep|当前平台使用的行终止符（Win下为'\r\n'，Linux下为'\n'）|
|os.name|指代当前使用的操作系统（包括：'posix',  'nt', 'mac', 'os2', 'ce', 'java'）|

##os.path模块中关于路径常用的函数使用方法
|函数名|使用方法|
|:---:|:---:|
|basename(path)|去掉目录路径，单独返回文件名|
|dirname(path)|去掉文件名，单独返回目录路径|
|join(path1[, path2[, ...]])|将path1, path2各部分组合成一个路径名|
|split(path)|分割文件名与路径，返回(f_path, f_name)元组。如果完全使用目录，它也会将最后一个目录作为文件名分离，且不会判断文件或者目录是否存在|
|splitext(path)|分离文件名与扩展名，返回(f_name, f_extension)元组|
|getsize(file)|返回指定文件的尺寸，单位是字节|
|getatime(file)|返回指定文件最近的访问时间（浮点型秒数，可用time模块的gmtime()或localtime()函数换算）|
|getctime(file)|返回指定文件的创建时间（浮点型秒数，可用time模块的gmtime()或localtime()函数换算）|
|getmtime(file)|返回指定文件最新的修改时间（浮点型秒数，可用time模块的gmtime()或localtime()函数换算）|
|以下函数返回True或者False||
|exists(path)|判断指定路径（目录或文件）是否存在|
|isabs(path)|判断指定路径是否为绝对路径|
|isdir(path)|判断指定路径是否存在且是一个目录|
|isfile(path)|判断指定路径是否存在且是一个文件|
|islink(path)|判断指定路径是否存在且是一个符号链接|
|ismount(path)|判断指定路径是否存在且是一个挂载点|
|samefile(path1, paht2)|判断path1和path2两个路径是否指向同一个文件| 
##异常
[常见的异常](https://fishc.com.cn/thread-45814-1-2.html)  
pickle的实质是利用计算机算法将数据对象压缩成二进制文件，类似于java的jar文件，可以供他人使用  
pickle使用pickle.dump（date，file）存储文件，第一个参数是待存储的数据对象，第二个参数是目标存储的文件对象，注意要先使用'wb'的模式open文件  
[__init__和self用法](https://blog.csdn.net/CLHugh/article/details/75000104)  
—init—类似于java中的构造函数  
self类似于java中的this指针  
如果我们不希望属性和方法被外部直接引用，我们可以在属性和方法名字前面加上双下划线，这样子外部就无法直接访问  
super函数可以用于多种继承，可以不用给它基类的名字，他会自动去调用合适的方法  
	    class BB:
	    def printBB():
	        print("no zuo no die")
	
	BB.printBB()#这时可以调用
	bb = BB()
	bb.printBB()#这时就不能调用了，因为Pyhon会把它改为bb.printBB(bb)所以构造方法中药加self
再举个列子

	    class CC:
        def setXY(self,x,y):
            self.x = x
            self.y = y
        def printXY(self):
            print(self.x,self.y)

    dd = CC()
    dd.__dict__#显示出是{}，一个空的字典
    CC.__dict__#显示出拥有很多东西的字典
    dd.setXY(4,5)#可以这样理解dd.setXY(dd,x,y)setXY方法就变成了dd.x = x dd.y = y
    dd.__dict__#显示出('y':5,'x':4)
    CC.__dict__#这时dd增加的没有出现在CC中，他们是独立的

***
[多重继承陷阱](https://fishc.com.cn/thread-48759-1-2.html)
[Python魔法方法](https://fishc.com.cn/thread-48793-1-2.html)
