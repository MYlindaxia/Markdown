#第一章	Maven项目
首先在Maven项目仓库中查找jar包（mvnrepository.com）
并将查到到的依赖信息复制到prom.xml中

#第二章 单元测试和JUnit
白盒测试：后端程序员，全面了解程序内部结构，对所有逻辑路径测试  
黑盒测试：完全不考虑程序内部结构和内部特性的情况下测试

自动测试：用程序自动批量，反复测试，并可自动检查功能。
手动测试：人工测试，很麻烦。

回归测试：修改旧代码后，重新进行测试以确认修改没有引入新的错误或导致其他代码产生错误。

测试策略：
- main方法测试 （分散程序员关注点，无法自动判断是否符和预期）
- JUnit测试 （简单，方便）

#第三章 高级文本处理
##Unicode（字符集）
- UTF8 兼容ASCII,变长（1-4个字节存储字符），经济，方便传输。
- UTF16 用变长（2-4个字节）来存储所有字符
- UTF32 用32bits（4个字节）存储所有字节

Java源文件采用UTF8编码，并且和外界输出尽量采用UTF8编码

##国际化编程

###Local类
- Locale
	1. 语言，zh，en等
	2. 国家/地区，CN，US等
- Locale方法
	1. getAvailableLocales()返回所有的可用Locale
	2. getDefault()返回默认的Locale

###语言文件命名规则：
- 包名+语言+国家地区.properties,(语言和国家地区可选)
- message.properies
- message_zh.properties
- message_zh_CN.properties

###语言文件
- 存储文件必须是ASCII码文件
- 如果是ASCII码以外的文字，必须用Unicode的表示\uxxxx
- 可以采用native2ascii.exe (%JAVA_HOME%\bin目录下)进行转码

###ResourceBundle类
- ResourceBundle
	1. 根据Locale要求，加载语言文件（Properties文件）
	2. 存储文件语言集合中所有的KV对
	3. getString（String key）返回所对应的值
- ResourceBundle根据key找value的查找路径
	- 包名_当前Locale语言_当前Locale国家地区_当前Locale变量(variant)
	- 包名_当前Locale语言_当前Locale国家地区
	- 包名_当前Locale语言
	- 包名_默认Locale语言_默认Locale国家地区_默认Locale变量(variant)
	- 包名_默认Locale语言_默认Locale国家地区
	- 包名_默认Locale语言
	- 包名

###正则表达式
java.util.regex包
 - Pattern 正则表达式编译表示
  - compile编译一个正则表达式为Pattern对象
  - matcher用Pattern对象匹配一个字符串，返回匹配结果
 - Matcher
  - Index Methods（位置方法） //start(),end()
  - Study Methods (查找方法）//lookingAt(),find(),matches()
  - Replacement Methods(替换方法) //replaceAll()

```java
public class TestFiles {
    private static final String REGEX = "\\bdog\\b";
    private static final String INPUT =  "dog dog dog doggie dogg";
    public static void main(String[] args) {
        Pattern pattern = Pattern.compile(REGEX);
        Matcher matcher = pattern.matcher(INPUT);
        int count = 0;
        while(matcher.find()){
            count++;
            System.out.println("Mathcer number" + count);
            System.out.println("start():"+ matcher.start());
            System.out.println("end():" + matcher.end());
        }
    }
}
```

###XML
XML是用来存储数据的，而不是显示数据
**所有XML文档都必须有一个根目录**
XML常规语法
- 任何的起始标签都必须有一个结束标签。
- 简化写法，例如，<name></name>可以写为<name/>。
- – 大小写敏感，如<name>和<Name>不一样。
- – 每个文件都要有一个根元素。
- 标签必须按合适的顺序进行嵌套，不可错位。
- 所有的特性都必须有值，且在值的周围加上引号。
- 需要转义字符，如“<”需要用&lt;代替。
- – 注释：<!-- 注释内容 --> 