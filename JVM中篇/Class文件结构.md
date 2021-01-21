## 概述

#### 一、字节码文件的跨平台性

1、Java语言：跨平台的语言(write one , run anywhere)

- 当java语言代码成功编译成字节码后，如果想要在不同的平台上面运行，则无需再次编译
- 这个优势不再那么吸引人了。Python、PHP、Perl、Ruby、Lisp等有强大的解释器。
- 跨平台似乎已经快成为一门语言必选的特性。

2、Java虚拟机：跨语言的平台

- Java虚拟机不和包括Java在内的任何语言绑定，它只与“Class文件”这种特定的二进制文件格式所关联。无论使用何种语言进行软件开发，只需要将源文件编译为正确的Class文件，那么这种语言就可以在Java虚拟机上执行。可以说，统一而强大的Class文件结构，就是Java虚拟机的基石、桥梁。![屏幕快照 2021-01-18 下午10.09.44](%E5%B1%8F%E5%B9%95%E5%BF%AB%E7%85%A7%202021-01-18%20%E4%B8%8B%E5%8D%8810.09.44.png)

- 官方规范地址：https://docs.oracle.com/javase/specs/index.html
- 所有的JVM全部遵守Java虚拟机规范，也就是说所有的JVM环境都是一样的，这样一来字节码文件可以在各种JVM上运行

3、想要让一个Java程序正确的运行在JVM中，Java源码就必须要被编译为符合JVM规范的字节码。

- 前端编译器的主要任务就是负责将符合Java语法规范非Java代码转化为符合JVM规范的字节码文件。
- javac是一种能够将Java源代码编译为字节码的前端编译器
- javac编译器在将Java源码编译为一个有效的字节码文件过程经历4个步骤，分别是==词====法解析、语法解析、语义解析以及生成字节码。==

![](%E5%B1%8F%E5%B9%95%E5%BF%AB%E7%85%A7%202021-01-18%20%E4%B8%8B%E5%8D%8810.26.32.png)

4、Oracle的JDK软件包括两部分内容：

- 一部分是将Java源代码编译成Java虚拟机的指令集的编译器
- 另一部分是将用于实现Java虚拟机的运行时环境

#### 二、Java的前端编译器

![](%E5%B1%8F%E5%B9%95%E5%BF%AB%E7%85%A7%202021-01-18%20%E4%B8%8B%E5%8D%8810.34.15.png)

1、前端编译器 vs 后端编译器

Java源代码的编译结果是字节码，那么肯定需要有一种编译器能够将Java源代码编译为字节码，承担这个重要责任的就是配置在path环境变量中的javac编译器。javac是一种能够将Java源代码编译为字节码的前端编译器。

HotSpot VM并没有强制要求前端编译器只能够使用javac来编译字节码，其中只要编译结构符合JVM规范都可以被JVM所识别即可。在Java的前端编译器领域，除了javac之外，还有一种被大家经常使用的前端编译器，那就是内置在Eclipse中的ECJ（Eclipse Compiler for Java）编译器。和javac的全量编译不同，ECJ是一种增量式编译器。

- 在Eclipse中，当开发人员编写完代码后，使用“Ctrl + S”快捷键时，ECJ编译器所采取的编译方案是把未编译部分的源代码逐行进行编译，而非每次都是全量编译。因此ECJ的编译效率会比javac更加的迅速和高效，当然编译质量和javac相比大致还是一样的。
- ECJ不仅仅是Eclipse的默认内置前端编译器，在Tomcat中同样也是使用ECJ编译器来编译jsp文件。由于ECJ编译器采用GPLv2的开源协议进行代码公开，所以，大家可以登录eclipse官网下载ECJ编译器的源代码进行二次开发。
- 默认情况下，IntelliJ IDEA使用javac编译器。（还可以自己设置为AspectJ编译器 ajc）

前端编译器并不会直接涉及编译优化等方面技术，而是将这些具体的优化细节移交给HotSpot的JIT编译器负责。

复习：AOT(静态提前编译器，Ahead Of Time Complier)

#### 三、透过字节码指令看代码细节

1、BAT面试题

- [ ] 类文件结构有几个部分

- [ ] 知道字节码吗？字节码都有哪些？Integer x = 5; int y = 5; 比较 x == y 都经过哪些步骤？

2、代码举例

例1:

```
/**
 * @author wanyi
 * @create 2021-01-18 23:09
 */
public class IntegerTest {
    public static void main(String[] args) {

        Integer x = 5;
        int y = 5;
        System.out.println(x == y);

        Integer i1 = 10;
        Integer i2 = 10;
        System.out.println(i1 == i2);// true

        Integer i3 = 128;
        Integer i4 = 128;
        System.out.println(i3 == i4);// false
    }
}
```

例2:

```
/**
 * @author wanyi
 * @create 2021-01-19 22:22
 */
public class StringTest {
    public static void main(String[] args) {

        String str = new String("hello") + new String("world");
        String str1 = "helloworld";
        System.out.println(str == str1);
    }
}
```

例3:

```
/**
 * @author wanyi
 * @create 2021-01-19 22:31
 */
public class SonTest {
    public static void main(String[] args) {
        Father f = new Son();
        System.out.println(f.x);
    }
}

class Father {
    int x = 10;

    public Father(){
        this.print();
        x = 20;
    }

    public void print(){
        System.out.println("Father.x = " + x);
    }
}

class Son extends Father{
    int x = 30;

    public Son(){
        this.print();
        x = 40;
    }

    public void print(){
        System.out.println("Son.x = " + x);
    }
}
```



## 虚拟机的基石：Class文件

#### 一、字节码文件里面是什么

源代码经过编译器编译之后便会生成一个字节码文件，字节码文件是一种二进制的类文件，它的内容是JVM的指令，而不像C、C++经过编译器直接生成机器码。

#### 二、什么是字节码指令

Java虚拟机的指令由一个字节长度的、代表着某种特定操作含义的操作码(opcode)以及跟随在其后的零至多个代表此操作所需要参数的操作数(operand)所构成。虚拟机中许多指令并不包括操作数，只有一个操作码。

比如：操作码 （操作数）

![](%E5%B1%8F%E5%B9%95%E5%BF%AB%E7%85%A7%202021-01-19%20%E4%B8%8B%E5%8D%8811.07.31.png)

#### 三、如何解读供虚拟机执行的二进制字节码

方式一：一个一个二进制的看。这里用到的是Notepad++，需要安装一个HEX-Editor插件，或者使用Binary Viewer

![](%E5%B1%8F%E5%B9%95%E5%BF%AB%E7%85%A7%202021-01-19%20%E4%B8%8B%E5%8D%8811.13.35.png)

方式二：使用javap指令：jdk自带的反解析工具

方式三：使用IDEA插件：jclasslib或jclasslib byte code viewer客户端工具。（可视化更好）

![](%E5%B1%8F%E5%B9%95%E5%BF%AB%E7%85%A7%202021-01-19%20%E4%B8%8B%E5%8D%8811.16.16.png)

或

![](%E5%B1%8F%E5%B9%95%E5%BF%AB%E7%85%A7%202021-01-19%20%E4%B8%8B%E5%8D%8811.16.27.png)



## Class文件结构

1、官方文档位置：https://docs.oracle.com/javase/specs/jvms/se8/html/jvms-4.html

2、class类的本质

- 任何一个Class文件都对应着唯一一个类或接口的定义信息，单反过来说，Class文件实际上它并不一定以磁盘文件的形式存在。Class文件是一组以8为字节为基础单位的二进制流。

3、Class文件格式

Class的结构不像Xml等描述语言，由于它没有任何分隔符号。所以在其中的数据项，无论是字节顺序还是数量，都是被严格想定的，哪个字节代表什么含义，长度是多少，先后顺序如何，都不允许改变。

Class文件格式采用一种类似于C语言结构体的方式进行数据存储，这种结构中只有两种数据类型：无符号数和表。

- 无符号数属于基本数据类型，以u1、u2、u4、u8来分别代表1个字节、2个字节、4个字节和8个字节的无符号数，无符号数可以用来描述数字、索引引用、数量值或者按照UTF-8编码构成字符串值。
- 表是由多个无符号数或者其他表作为数据项构成的复合数据类型，所有表都习惯性地以“_info”结尾。表用于描述有层次关系的复合结构的数据，整个Class文件本质上就是一张表，由于表没有固定的长度，所以通常会在其面前加上个数说明。

代码举例：

```
/**
 * @author wanyi
 * @create 2021-01-20 21:56
 */
public class Demo {

    private int num = 1;

    public int add(){
        num = num + 2;
        return num;
    }
}
```

对应字节码文件：

![](%E5%B1%8F%E5%B9%95%E5%BF%AB%E7%85%A7%202021-01-20%20%E4%B8%8B%E5%8D%8810.04.00.png)

换句话说，充分理解了每一个字节码文件的细节，自己也可以反编译出Java源文件来。

4、class文件结构概述

Class文件的结构并不是一成不变的，随着Java虚拟机的不断发展，总是不可避免地会对Class文件结构作出一些调整，但是其基本结构和框架是非常稳定的。

Class文件的总体结构如下：

- 魔数
- Class文件版本
- 常量池
- 访问标记
- 类索引、父类索引、接口索引集合
- 字段表集合
- 方法表集合
- 属性表集合

![](%E5%B1%8F%E5%B9%95%E5%BF%AB%E7%85%A7%202021-01-20%20%E4%B8%8B%E5%8D%8810.14.06.png)

![](%E5%B1%8F%E5%B9%95%E5%BF%AB%E7%85%A7%202021-01-20%20%E4%B8%8B%E5%8D%8810.16.52.png)

#### 一、Magic Number(魔数)

- 每个Class文件开头的4个字节的无符号整数称为魔数（Magic Number）
- 它的唯一作用是确定这个文件是否为一个能被虚拟机接受的有效合法的Class文件。即：魔数是Class文件的标识符。
- 魔数值固定为0xCAFEBABE。不会改变
- 如果一个Class文件不以0xCAFEBABE开头，虚拟机在进行文件校验的时候就会直接抛出以下错误：

```
错误: 加载主类 Demo1 时出现 LinkageError
java.lang.ClassFormatError: Incompatible magic value 1885430635 in class file Demo1
```

- 使用魔数而不是扩展名来进行识别主要是基于安全方面的考虑，因为文件的扩展名可以随意地改动。

#### 二、Class文件的版本号

- 紧接在魔数的4个字节存储的是Class文件的版本号。同样也是4个字节。第5和第6个字节所代表的含义就是编译的副版本号minor_version，而第7和第8个字节就是编译的主版本号major_version。
- 它们共同构成了class文件的格式版本号。譬如某个Class文件的主版本号为M，副版本号为m，那么这个Class文件的格式版本号就确定为M.m。
- 版本号和Java编译器的对应关系如下表：

![](%E5%B1%8F%E5%B9%95%E5%BF%AB%E7%85%A7%202021-01-21%20%E4%B8%8B%E5%8D%8810.09.53.png)

- Java的版本号是从45开始的，JDK1.1之后的每个JDK大版本发布主版本号向上加1.
- 不同版本的Java编译器编译的Class文件对应的版本是不一样的。目前，最高版本的Java虚拟机可以执行由低版本编译器生成的Class文件，但是低版本的Java虚拟机不能执行由高版本编译器生成的Class文件。否则Java虚拟机会抛出java.lang.UnsupportedClassVersionError异常。（向下兼容）
- 在实际应用中，由于开发环境和生产环境的不同，可能会导致该问题的发生。因此，需要我们在开发时，特别注意开发编译的JDK版本和生产环境的JDK版本是否一致。
- 虚拟机JDK版本为1.k（k>2）时，对应的class文件格式版本号的范围为45.0 - 44+k.0（含两端）

#### 三、常量池：存放所有常量

- 常量池是Class文件中内容最为丰富的区域之一。常量池对于Class文件中字段和方法解析也有至关重要的作用。
- 随着Java虚拟机的不断发展，常量池的内容也日渐丰富。可以说，常量池是整个Class文件的基石。

![](%E5%B1%8F%E5%B9%95%E5%BF%AB%E7%85%A7%202021-01-21%20%E4%B8%8B%E5%8D%8810.23.45.png)

- 在版本号之后，紧跟着的是常量池的数量，以及若干个常量池表项。
- 常量池中的常量的数量是不固定的，所以在常量池的入口需要放置一项u2类型的无符号数，代表常量池容量计数值(constant_pool_count)。与java中语言习惯不一样的是，这个容量计数是从1开始而不是0开始的。

![](%E5%B1%8F%E5%B9%95%E5%BF%AB%E7%85%A7%202021-01-21%20%E4%B8%8B%E5%8D%8810.30.54.png)

- 由上表可见，Class文件使用了一个前置的容量计数器(constant_pool_count)加上若干个连续的数据项(constant_pool)的形式来描述常量池内容。我们把这一系列连续常量池数据称为常量池集合。
- 常量池表项中，用于存放编译时期生成的各种字面量和符号引用，这部分内容将在类加载后进入方法区的运行时常量池中存放。

1、constant_pool_count（常量池计数器）

- 由于常量池的数量不固定，是长是短，所以需要放置两个字节来表示常量池容量计数值。
- 常量池容量计数值(u2类型)：从1开始，表示常量池中有多少项常量。即constant_pool_count=1表示常量池中有0个常量项。
- Demo的值为：

![](%E5%B1%8F%E5%B9%95%E5%BF%AB%E7%85%A7%202021-01-21%20%E4%B8%8B%E5%8D%8810.48.36.png)

- 其值为0x0016，掐指一算，也就是22.
- 需要注意的是，这实际上只有21项常量。索引范围为1-21。为什么呢？

```
通常我们写代码是都是从0开始的，但是这里的常量池却是从1开始，因为它把第0项常量空出来了。这是为了满足后面某些指向常量池的索引值的数据在特定情况下需要表达“不引用任何一个常量池项目”的含义，这种情况可用索引值0来表示
```

