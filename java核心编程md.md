#第二章
##储存到什么地方
- 寄存器：最快的存储区，在处理器内部，容器及其有限！
- 堆栈：用于存放数据
- 堆：用于存放对象
- 常量存储：直接存放在代码内部
##高精度数字
Biginteger：整数 BigDecimal:小数  
他们和基本类型拥有相同的方法，也就是说能用于int和float的操作他们都能，不过只能用方法调用，我们这里用速度换取精度  
##return的奇葩作用
在方法声明为void中，可以使用return来结束该方法
##static的作用
1. static用于方法可以让方法直接归输入类
2. static用于域可以让该域在每个类中只有一份存储空间
##神奇的编码风格
- 包名全部小写
- 类名首字母大写，而且不要以下划线来分割两个单词
- 方法，字段，对象的引用都首字母小写
- 常量全部大写并尽量详细，每个单词以下划线分开
##严肃的JavaDoc
- @see 表示引用的其他外部文档
- @docRoot 用于文档界面显示超链接
- @version 表示当前版本
- @author 表示当前文档的作者
- @since 表示使用的JDK版本
- @parm 表示参数的意思
- @return 表示返回值的意思
- @throws 表示抛出什么异常
- @deprecated 表示当前方法可能会在以后的版本被删除，告诉使用者不要在继续使用这个方法

#第三章
##神奇的赋值（别名引用）
java在基本类型中赋值只是将内容复制给对方。而如果是对象赋值则是将引用赋值给对方，双方修改任何值对方对应的值也会被修改。  
```java
class T1{
    String s;
}
public class TestString {
    public static void main(String[] args) {
        T1 t1 = new T1();
        T1 t2 = new T1();
        t1.s = "MYlindaxia";
        t1 = t2;
		//避免别名现象
		t1.s = t2.s;
        t2.s = "123";
        System.out.println(t1.s);
        System.out.println(t2.s);
    }
}
```
##神奇的按位操作符
按位操作符用32位的0和1表示，最前面的一位是符号判断，如果是0则是正数，如果是1就是负数。  
&表示将两个数字分成32位，然后每位依次对比，如果两个都是1则输出1，否则输出0  
|如果两个数字中只要有一个是1，则输出1，否则输出0
~表示取反操作，是一元操作符，只能对一个数字使用。  
^异或操作符，如果两个数字中有一个是1但不全是1则输出1.
##移位操作符
    <<能将右侧指定的位数向前移动，左低位补0
    >>能将左侧指定位数向右移动，若符号为正，则在高位插入0，若符号为负，则插入1.
    >>>无符号右移操作符，不管正负，都在高位插入0
移位操作符都是按照补码来移动位置的，java中原码有32位，第一位为符号位，0为正数，1为负数。  
举例：
```java
原码：1000 0000 0000 0000 0000 0000 0000 0101	正数原码反码补码都一样
反码：1111 1111 1111 1111 1111 1111 1111 1010	反码符号位不变其他取反
补码：1111 1111 1111 1111 1111 1111 1111 1011	补码最后一位加一
```
##简单但却孤独的三元操作符
```java
public class TestString {
    public static void main(String[] args) {
        int i = 1 > 2 ? 123 : 312;
        System.out.println(i);
    }
}
```
##搞怪的类型转换
java可以通过强转型来转换类型  
```java
public class TestString {
    public static void main(String[] args) {
        int i = 123;
        double d = (double)i;
        System.out.println(d);
    }
}
//output：123.0
```
如果是小数转型为整数，则会进行截尾操作,但我们可以通过java.lang.Math中的round方法来进行四舍五入。
```java
public class TestString {
    public static void main(String[] args) {
        double d = 123.321;
        float f = 123.5f;
        int i1 = (int)d;
        int i2 = (int)f;
        System.out.println(i1);
        System.out.println(i2);

    }
}
//output:
123
123
```
###提升
如果将一个float的值和double的值相乘，结果就是double类型的，如果将一个int和一个long类型相加，结果就是long类型。

##第四章 控制执行流程
do-while语法结构
```java
	do{
		statement}
	while(判断);
```
逗号操作符：java里唯一用到逗号操作符的地方就是在for循环里，在初始化和控制步进的规则里可以使用，而他们会独立执行
```java
        for(int i = 0, j = 1;i<=10;i++,j++){
            System.out.println(i+j);
        }
```
###严格的return
return关键词有两个作用：
1. 指定一个方法返回什么值
2. 导致当前方法退出，并返回那个值。
###臭名昭著的Goto
```java
        lable1:
            for(int j = 1;j<10;j++){
                label2:
                for(int i = 0;i<10;i++){
                    if (j == 5){
                        continue lable1;
                    }
                    System.out.println("现在i是"+i+"j是"+j);
                }
            }
```
**要记住的重点是：在java中使用标签的唯一理由是应为有多重循环嵌套存在，而且想从多层嵌套中break或continue**
###好用但很孤独的Switch
```java
//基本语法
	        int i = 1;
        switch (i){
            case 1:
                System.out.println("1");
                break;
            case 2:
                System.out.println("2");
                break;
            case 3:
                System.out.println("3");
                break;
            case 4:
                System.out.println("4");
                break;
            default:
                System.out.println("5");
        }
```
**超级兴奋,在JAVA5之前switch只支持int数字，5之后可以支持字符串了！！！，但是还是不支持小数**
###提升（小技巧，产生随机字母)
```java
    Random rand = new Random(27);
for(int i = 0;i<100;i++){
    int c = rand.nextInt(26) + 'a';
    System.out.println((char)c);
}
```
##第五章 初始化与清理（重点）
###容易出错的方法重载
在java中，参数顺序不同也可以区分两个方法，但请别这么做，这会使代码难以维护
*涉及基本类型的重载，由于代码太多，而且本人没搞多清楚，就先放在这里。页数为：79页*  

```java  
package com.lianxi5;

import static net.mindview.util.Print.*;

public class PrimitiveOverloading {
    //f1方法start
    void f1(char x) {
        print("f1(char)");
    }

    void f1(byte x) {
        print("f1(byte)");
    }

    void f1(short x) {
        print("f1(short)");
    }

    void f1(int x) {
        print("f1(int)");
    }

    void f1(long x) {
        print("f1(long)");
    }

    void f1(float x) {
        print("f1(float)");
    }

    void f1(double x) {
        print("f1(double)");
    }
    //f1方法stop，f2方法start
    void f2(byte x) {
        print("f2(byte)");
    }

    void f2(short x) {
        print("f2(short)");
    }

    void f2(int x) {
        print("f2(int)");
    }

    void f2(long x) {
        print("f2(long)");
    }

    void f2(float x) {
        print("f2(float)");
    }

    void f2(double x) {
        print("f2(double)");
    }
    //f2方法stop，f3方法start
    void f3(short x) {
        print("f3(short)");
    }

    void f3(int x) {
        print("f3(int)");
    }

    void f3(long x) {
        print("f3(long)");
    }

    void f3(float x) {
        print("f3(float)");
    }

    void f3(double x) {
        print("f3(double)");
    }
    //f3方法stop，f4方法start
    void f4(int x) {
        print("f4(int)");
    }

    void f4(long x) {
        print("f4(long)");
    }

    void f4(float x) {
        print("f4(flaot)");
    }

    void f4(double x) {
        print("f4(double)");
    }
    //f4方法stop，f5方法start
    void f5(long x) {
        print("f5(long)");
    }

    void f5(float x) {
        print("f5(flaot)");
    }

    void f5(double x) {
        print("f5(double)");
    }
    //f5方法stop，f6方法start
    void f6(float x) {
        print("f6(flaot)");
    }

    void f6(double x) {
        print("f6(double)");
    }
    //f6方法stop，f7方法start
    void f7(double x) {
        print("f7(double)");
    }

    void testConstVal() {
        print("5: ");
        f1(5);
        f2(5);
        f3(5);
        f4(5);
        f5(5);
        f6(5);
        f7(5);
        print();
    }

    void testChar() {
        char x = 'x';
        print("char: ");
        f1(x);
        f2(x);
        f3(x);
        f4(x);
        f5(x);
        f6(x);
        f7(x);
        print();
    }
    void testByte(){
        byte x = 0;
        print("byte: ");
        f1(x);
        f2(x);
        f3(x);
        f4(x);
        f5(x);
        f6(x);
        f7(x);
        print();
    }

    void testShort() {
        short x = 0;
        print("short: ");
        f1(x);
        f2(x);
        f3(x);
        f4(x);
        f5(x);
        f6(x);
        f7(x);
        print();
    }

    void testInt() {
        int x = 0;
        print("int: ");
        f1(x);
        f2(x);
        f3(x);
        f4(x);
        f5(x);
        f6(x);
        f7(x);
        print();
    }

    void testLong() {
        long x = 0;
        print("long: ");
        f1(x);
        f2(x);
        f3(x);
        f4(x);
        f5(x);
        f6(x);
        f7(x);
        print();
    }

    void testFloat() {
        float x = 0;
        print("float: ");
        f1(x);
        f2(x);
        f3(x);
        f4(x);
        f5(x);
        f6(x);
        f7(x);
        print();
    }

    void testDouble() {
        double x = 0;
        print("double: ");
        f1(x);
        f2(x);
        f3(x);
        f4(x);
        f5(x);
        f6(x);
        f7(x);
        print();
    }

    public static void main(String[] args) {
        PrimitiveOverloading p = new PrimitiveOverloading();
        p.testConstVal();
        p.testChar();
        p.testByte();
        p.testShort();
        p.testInt();
        p.testLong();
        p.testFloat();
        p.testDouble();
    }
}
//output：
5: 
f1(int)
f2(int)
f3(int)
f4(int)
f5(long)
f6(flaot)
f7(double)

char: 
f1(char)
f2(int)
f3(int)
f4(int)
f5(long)
f6(flaot)
f7(double)

byte: 
f1(byte)
f2(byte)
f3(short)
f4(int)
f5(long)
f6(flaot)
f7(double)

short: 
f1(short)
f2(short)
f3(short)
f4(int)
f5(long)
f6(flaot)
f7(double)

int: 
f1(int)
f2(int)
f3(int)
f4(int)
f5(long)
f6(flaot)
f7(double)

long: 
f1(long)
f2(long)
f3(long)
f4(long)
f5(long)
f6(flaot)
f7(double)

float: 
f1(float)
f2(float)
f3(float)
f4(flaot)
f5(flaot)
f6(flaot)
f7(double)

double: 
f1(double)
f2(double)
f3(double)
f4(double)
f5(double)
f6(double)
f7(double)

```
***总结：  
如果传入的参数小于方法里面的参数，实际数据类型会慢慢提升，整数慢慢提升到最大整数long，然后在提升到浮点数float和double（char类型有些不同）如果它无法找到刚好接受char参数的方法，它会直接“跳级”到int类型***  
```java
package com.lianxi5;

import static net.mindview.util.Print.print;

public class Test {
    void f1(char x) {
        print("f1(char)");
    }

    void f1(byte x) {
        print("f1(byte)");
    }

    void f1(short x) {
        print("f1(short)");
    }

    void f1(int x) {
        print("f1(int)");
    }

    void f1(long x) {
        print("f1(long)");
    }

    void f1(float x) {
        print("f1(float)");
    }

    void f1(double x) {
        print("f1(double)");
    }

    //f1方法stop，f2方法start
    void f2(char x) {
        print("f2(char)");
    }

    void f2(byte x) {
        print("f2(byte)");
    }

    void f2(short x) {
        print("f2(short)");
    }

    void f2(int x) {
        print("f2(int)");
    }

    void f2(long x) {
        print("f2(long)");
    }

    void f2(float x) {
        print("f2(float)");
    }

    //f2方法stop，f3方法start
    void f3(char x) {
        print("f3(char)");
    }

    void f3(byte x) {
        print("f3(byte)");
    }

    void f3(short x) {
        print("f3(short)");
    }

    void f3(int x) {
        print("f3(int)");
    }

    void f3(long x) {
        print("f3(long)");
    }

    void f4(char x) {
        print("f4(char)");
    }

    void f4(byte x) {
        print("f4(byte)");
    }

    void f4(short x) {
        print("f4(short)");
    }

    void f4(int x) {
        print("f4(int)");
    }

    void f5(char x) {
        print("f5(char)");
    }

    void f5(byte x) {
        print("f5(byte)");
    }

    void f5(short x) {
        print("f5short()");
    }

    void f6(char x) {
        print("f6(char)");
    }

    void f6(byte x) {
        print("f6(byte)");
    }

    void f7(char x) {
        print("f7(char)");
    }

    void testDouble() {
        double x = 0;
        print("double argument:");
        f1(x);
        f2((float) x);
        f2((long) x);
        f2((int) x);
        f2((short) x);
        f2((byte) x);
        f2((char) x);
    }

    public static void main(String[] args) {
        Test t = new Test();
        t.testDouble();
    }
}
output:
double argument:
f1(double)
f2(float)
f2(long)
f2(int)
f2(short)
f2(byte)
f2(char)
```
***总结：
当传入参数类型大于方法里的参数时，必须进行窄化转换，不然就报错啦***
###神奇的This指针
 1. This不仅可以用来指代当前对象的某个属性或方法，它还可以直接指代当前对象
 2. **This还可以在构造器中调用本类中的其他构造器（必须在构造方法中使用，而且必须放在代码的第一行）**  

```java
package com.lianxi5;

class Person {
    public void eat(Apple apple) {
        Apple peeled = apple.getPeeled();
        System.out.println("Yummy");
    }
}

class Peeler {
    static Apple peel(Apple apple) {
        return apple;
    }
}

class Apple {
    Apple getPeeled() {
        return Peeler.peel(this);
    }
}

public class PassingThis {
    public static void main(String[] args) {
        new Person().eat(new Apple());
    }
}

```
----
```java
package com.lianxi5;

public class TestThis {
    public TestThis(){
        //必须放在第一行
        this("hi");
        System.out.println("这是无参构造器，调用本类中的有参数构造器");
    }
    public TestThis(String s){
        System.out.println(s);
        System.out.println("恭喜你调用了有参构造器");
    }
    public void test(){
//        错误，只能在构造方法中用this调用其他构造器，而且必须放在第一行
//        this("hi");
    }

}
  
```
##强大的static
在static方法中不能调用非static方法，而非静态方法可以调用static方法。  
static的主要用途就是在没有创建对象时仅仅通过本身的类来调用static方法
###神奇的清理（重点）
java的垃圾回收期只知道释放那些通过new分配的内存，如果你通过一个特殊方法，获得了一块内存，需要通过finalize（）方法来回收  
它的原理是这样：一旦垃圾回收器准备释放资源，将首先调用finalize（）方法，并在下一次垃圾回收动作发生时，才会真正回收对象占用的内存。  
**在java中，对象可能不会被垃圾回收**  
**垃圾回收并不等于“析构函数”**
####finalize（）真正的用途
 1. 垃圾回收期只与内存有关（调用垃圾回收期的唯一原因就是回收程序不再使用的内存）
 2.  在java中，对象可能不会被垃圾回收 
 3.  垃圾回收并不等于“析构函数
***无论是“垃圾回收”还是“终结(finalize)”，都不保证会发生。如果java虚拟机（JVM）并未面临内存耗尽的情况，它不会浪费时间去执行垃圾回收以恢复内存的（他们都靠不住）***
finalize有一个有趣的特点：它并不依赖于每次都要对finalize（）进行调用，这就是对象总结条件的验证(应该是可以在finalize方法里面加上逻辑判断)。当某一个对象被释放时，应当可以安全被释放，要是对象代表了一个文件，在对象被回收前应当关闭这个文件，如果没有关闭就会发生错误。finalize可以用来发现这种情况，尽管它并不总是会被调用
###提升（不同JVM中回收机制的不同情况）
参考书：p90  
参考连接：[不同JVM的回收机制](https://www.cnblogs.com/aspirant/p/8662690.html)

###初始化（重点）
在类里面定义一个对象的引用时，如果不对其进行初始化，则会自动获得一个null值。  
可以通过方法甚至有参方法进行初始化（前提是参数必须已经初始化了）  

```java
int i = f();
int f(){
return 11;}
```