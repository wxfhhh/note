[TOC]


# File类

## 概述

`java.io.File`类

文件和目录路径名的抽象表示形式。
java把电脑中的文件和文件夹(目录)封装为一个File类,我们可以使用File类对文件和文件夹进行操作

我们可以使用File类的方法

- 创建一个文件/文件夹删除文件/文件夹获取文件/文件夹

- 判断文件/文件夹是否存在对文件夹进行遍历

- 获取文件的大小

  File类是一个与系统无关的类,任何的操作系统都可以使用这个类中的方法

  重点:记住这三个单词

  file:文件

  directory:文件夹/目录

  path :路径

## File类的静态成员变量

`static string pathSeparator`与系统有关的路径分隔符，为了方便，它被表示为一个字符串。

`static char pathSeparatorChar`与系统有关的路径分隔符。
`static String separator`与系统有关的默认名称分隔符，为了方便，它被表示为一个字符串。

`static char separatorChar`与系统有关的默认名称分隔符。
操作路径:**注意** 路径不能写死了
c: \develop\a\a.txt   **windows**

c: /develop/a/a.txt    **linux**

"C: "+`FiLe.separator`+ " develop"+`FiLe.separator`+"a"+`File.separator`+"a.txt"

> 路径分格符    windows： 分号 ;     linux:冒号 :
>
> 文件名称分隔符： windows:反斜杠 |  linux:正斜杠 /

## 绝对路径和相对路径

路径:
绝对路径:是一个完整的路径
以盘符(c:  ,D:)开始的路径
c : \\\a.txt
c: \\ \Users\itcast\\\IdeaProjects\\\shungyuan \ \\123.txtD: l ldemollb.txt
相对路径:是一个简化的路径
相对指的是相对于当前项目的根目录(C:\\\Users\itcast\IdeaProjects \\\shungyuan)如果使用当前项目的根目录,路径可以简化书写
c:\\\Users\itcast\\\IdeaProjects\\\shungyuan\\\123.txt--><font color=red>简化为:</font>
123.txt(可以省略项目的根目录)
注意:
1.路径是不区分大小写的
⒉路径中的文件名称分隔符windows使用反斜杠,反斜杠是转义字符,两个反斜杠代表一个普通的反斜杠

## File类的构造方法

1.`File(String pathname）` 通过将给定路径名字符串转换为抽象路径名来创建一个新File实例。

参数:
`String pathname`:字符串的路径名称
路径可以是以文件结尾,也可以是以文件夹结尾

路径可以是相对路径,也可以是绝对路径
路径可以是存在,也可以是不存在
<!--创建File对象，只是把字符串路径封装为File对象,不考虑路径的真假情况(不管有没有这个路径都会打印执行)-->

2.`File(String parent，String child）`根据parent路径名字符串和 child 路径名字符串创建一个新File 实例。

参数:

把路径分成了两部分

string parent:父路径

string child:子路径

好处:
父路径和子路径,可以单独书写,使用起来非常灵活;父路径和子路径都可以变化

3.`File(File parent，String child)`根据parent抽象路径名和child路径名字符串创建一个新File实例。

参数:

把路径分成了两部分

File parent:父路径

string child:子路径

好处:
父路径和子路径,可以单独书写,使用起来非常灵活;父路径和子路径都可以变化

父路径是File类型,可以使用File的方法对路径进行一些操作,再使用路径创建对象

## File类的方法

### 获取功能的方法

`public string getAbsolutePath()`:返回此File的绝对路径名字符串。

> 获取的构造方法中传递的路径
> 无论路径是绝对的还是相对的, getAbsolutePath方法返回的都是绝对路径

`public String getPath() `:将此File转换为路径名字符串。

> 获取的构造方法中传递的路径
> toString方法调用的就是getPath方法
>
> 源码:
> public string toString( ) {
> return getPath( );
>
> }

`public string getName()` :返回由此File表示的文件或目录的名称。

> 获取的就是构造方法传递路径的结尾部分(文件/文件夹)

`public long length()`:返回由此File表示的文件的长度。

> 获取的是构造方法指定的文件的大小,以字节为单位
>
> 注意:
> 文件夹是没有大小概念的,不能获取文件夹的大小
> 如果构造方法中给出的路径不存在,那么Length方法返回0

### 判断功能的方法

`public boolean exists()` :此FiLe表示的文件或目录是否实际存在。用于判断               构造方法中的路径是否存在
			存在:true
			不存在:false

`public boolean isDirectory()` :此FiLe表示的是否为目录。
用于判断构造方法中给定的路径是否以文件夹结尾
		是:true
		否:false
`public boolean isFile() `: 此File表示的是否为文件。
用于判断构造方法中给定的路径是否以文件结尾
		是:true
		否:false
注意:
电脑的硬盘中只有文件/文件夹,两个方法是互斥
这两个方法使用前提,**路径必须是存在的**,否则都返回false

### 创建和删除的方法

`public boolean createNewFile()`:当且仅当具有该名称的文件尚不存在时，创建一个新的空文件。创建文件的路径和名称在构造方法中给出(构造方法的参数)
返回值:布尔值
true:文件不存在,创建文件,返回true

false:文件存在,不会创建,返回false

注意:

> 1.此方法只能创建文件,不能创建文件夹
>
> 2.创建文件的路径必须存在,否则会抛出异常
> public boolean createNewFile( ) throws IOException
> createNewFiLe声明抛出了IOException,我们调用这个方法,就必须的处理这个异常,要么throws,要么try...catch

`public boolean mkdir() `:创建单级空文件夹
`public boolean mAdirs()`:既可以创建单级空文件夹,也可以创建多级文件夹

创建文件夹的路径和名称在构造方法中给出(构造方法的参数)
返回值:布尔值
true:文件夹不存在,创建文件夹,返回true
false:文件夹存在,不会创建,返回faLse;构造方法中给出的路径不存在返回false

注意:此方法只能创建文件夹,不能创建文件

`public boolean delete()` :删除由此FiLe表示的文件或目录。此方法,可以删除构造方法路径中给出的文件/文件夹
返回值:布尔值
	true:文件/文件夹删除成功,返回true
	false:文件夹中有内容,不会删除返回false;构造方法中路径不存在false

注意:delete方法是直接在硬盘删除文件/文件夹,不走回收站,<font color=red>删除要谨慎</font>

### 遍历(文件夹)目录的功能

`public String[ ] list()`:返回一个string数组，表示该File目录中的所有子文件或目录。

`public File[] listFiles()`:返回一个File数组，表示该File目录中的所有的子文件或目录。

> 注意:
> List方法和ListFiles方法遍历的是构造方法中给出的目录
>
> 如果构造方法中给出的目录的路径不存在,会抛出空指针异常
>
> 如果构造方法中给出的路径不是一个目录,也会抛出空指针异常

# 递归

## 概述

递归:方法自己调用自己

- -递归的分类:

  -递归分为两种，直接递归和间接递归。

  -直接递归称为方法自身调用自己。
  -间接递归可以A方法调用B方法，B方法调用c方法，c方法调用A方法。

- -注意事项:

  -递归一定要有条件限定，保证递归能够停止下来，否则会发生**栈内存溢出**。

  -在递归中虽然有限定条件，但是递归次数不能太多。否则也会发生**栈内存溢出**

  -**构造方法,禁止递归**

- 递归的使用前提:

  当调用方法的时候,方法的主体不变,每次调用方法的参数不同,可以使用递归

## 练习

1. 计算1~n的累计和

   注意:
   使用递归求和,main方法调用sum方法,sum方法会一直调用sum方法
   导致在内存中有多个sum方法(频繁的创建方法,调用方法,销毁方法)效率低下
   所以如果仅仅是计算1-n之间的和不推荐使用递归,使用for循环即可

2. 用递归计算阶乘

3. 用递归遍历打印多级目录

4. ![](https://i.bmp.ovh/imgs/2022/01/f5d64d44f4256f42.png)

   会发现打印得不够完整

5. 文件搜索

   只打印特定的文件名

   

   

   

# 过滤器（文件搜索）

我们可以使用过滤器来实现
在File类中有两个和ListFiles重载的方法,方法的参数传递的就是过滤器

## FileFilter

`File[] listFiles(FileFilter filter)`
`java.io.FileFilter接口`:用于抽象路径名(File对象)的过滤器。
作用:用来过滤文件(File对象)
抽象方法:用来过滤文件的方法
`boolean accept(File pathname）`测试指定抽象路径名是否应该包含在某个路径名列表中。参数:
File pathname:使用ListFiles方法遍历目录,得到的每一个文件对象

> listFiles方法一共做了3件事情:
> 1.listFiles方法会对构造方法中传递的目录进行遍历,获取目录中的每一个文件/文件夹-->封装为File对象
>
> 2.listFiles方法会调用参数传递的过滤器中的方法accept
> 3.listFiles方法会把遍历得到的每一个File对象,传递过accept方法的参数pathname
>
> 必须明确两件事情:
> accept方法返回值是一个布尔值
> 1.过滤器中的accept方法是谁调用的
> 2.accept方法的参数pathname是什么?
>
> accept方法返回值是一个布尔值
> 'rue:就会把传递过去的File对象保存到File数组中
> false:就不会把传递过去的File对象保存到File数组中

```java
 private static void getAllFile(File f) {
                File[] files = f.listFiles(new FileFilter(){
                    @Override
                    public boolean accept(File pathname) {
                        return pathname.isDirectory()||                       pathname.getPath().toLowerCase().endsWith(".bmp");
                    }
                });
```



## FilenameFilter

`FiLe[] listFiles ( FiLenameFilter filter)`
java.io.FiLenameFilter接口:实现此接口的类实例可用于过滤器文件名。
作用:用于过滤文件名称
抽象方法:用来过滤文件的方法
boolean accept(File dir,String name）测试指定文件是否应该包含在某一文件列表中。参数:
File dir:构造方法中传递的被遍历的目录
String name:使用ListFiles方法遍历目录,获取的每一个文件/文件夹的名称
注意:
两个过滤器接口是没有实现类的,需要我们自己写实现类,重写过滤的方法accept,在方法中自己定义过滤的规则

```java
//FilenameFilter
    private static void getAllFile(File f) {
        File[] files = f.listFiles(new FilenameFilter(){
            @Override
            public boolean accept(File dir,String name) {
               return new File(dir,name).isDirectory() ||
                        name.toLowerCase().endsWith(".bmp");
           }
        });
```



## Lambda表达式优化

```java
 private static void getAllFile(File f) {
//        File[] files = f.listFiles((dir,name)->
//                new File(dir,name).isDirectory()||name.toLowerCase().endsWith(".bmp"));
    File[] files = f.listFiles(pathname->           pathname.isDirectory()||pathname.getPath().toLowerCase().endsWith(".bmp"));
        for (File file : files) {
            if (file.isDirectory()) {
                getAllFile(file);
            } else {
                System.out.println(file);
            }

```

# IO流

## 概述

i：input  输入（读取）

o：output 输出（写入）

流：数据（字符，字节）  1个字符=2个字节  1个字节=8个二进制

输入：把硬盘中的数据，读取到内存中使用

输出：把内存中的数据，写入到硬盘中保存

|        | 输入流                | 输出流                 |
| ------ | --------------------- | ---------------------- |
| 字节流 | 字节输入流InputStream | 字节输出流OutputStream |
| 字符流 | 字符输入流Reader      | 字符输出流Writer       |

## 字节流

### 一切皆为字节

一切文件数据(文本、图片、视频等)在存储时，都是以二进制数字的形式保存，都一个一个的字节，那么传输时一样如此。所以，字节流可以传输任意文件数据。在操作流的时候，我们要时刻明确，无论使用什么样的流对象，底层传输的始终为二进制数据。

### 字节输出流

#### OutputStream类

`java.io.outputstream`:字节输出流
此抽象类是表示输出字节流的所有类的超类。定义了一些子类共性的成员方法:

- `public void close()`:关闭此输出流并释放与此流相关联的任何系统资源。

- ` public void flush( )`:刷新此输出流并强制任何缓冲的输出字节被写出。

- `public void write(byte[] b)`:将b.length字节从指定的字节数组写入此输出流。

- `public void write(byte[ ] b,int off, int len)`:从指定的字节数组写入len字节，从偏移量off开始输出到此输出流。

  int off:索引值
  int len:写几个字节

- `public abstract void write(int b)`:将指定的字节输出流。

#### FileOutputStream类

`java.io.FileOutputStream extends OutputStream`
FileOutputStream:文件字节输出流
作用:把内存中的数据写入到硬盘的文件中

**构造方法**:

`FiLeOutputStream(String name)`:创建一个向具有指定名称的文件中写入数据的输出文件流。
`FileOutputStream(File file)`:创建一个向指定File对象表示的文件中写入数据的文件输出流。

参数:写入数据的目的地
string name:目的地是一个文件的路径

File file:目的地是一个文件
构造方法的作用:
1.创建一个FileOutputStream对象
2.会根据构造方法中传递的文件/文件路径,创建一个空的文件

3.会把FileOutputStream对象指向创建好的文件

**写入数据的原理(内存-->硬盘)**
java程序-->JVM(java虚拟机)-->oS(操作系统)-->os调用写数据的方法-->把数据写入到文件中

**使用步骤(重点)**:
1.创建一个FileOutputStream对象,构造方法中传递写入数据的目的地

2.调用FileOutputStream对象中的方法write,把数据写入到文件中
3.释放资源(流使用会占用一定的内存,使用完毕要把内存清空,提供程序的效率)close();

#### 续写和换行

追加写/续写:使用两个参数的构造方法
`FiLeOutputStream(String name， booLean append)`创建一个向具有指定name的文件中写入数据的输出文件流。

`FileOutputStream(File file， boolean append)`创建一个向指定FiLe对象表示的文件中写入数据的文件输出流。

参数:

> string name,File file:写入数据的目的地
>
> boolean append :追加写开关
> true:创建对象不会覆盖源文件,继续在文件的末尾追加写数据
>
> false:创建一个新文件,覆盖源文件

写换行:写换行符号

windows : \r\n

linux:/n
mac:/r

```java
fos1.write("\r\n".getBytes());
```

### 字节输入流

#### InputStream类

`java.io.Inputstream`:字节输入流
此抽象类是表示字节输入流的所有类的**超类**。
定义了所有子类共性的方法:
`int read()`从输入流中读取数据的下一个字节。
`int read(byte[] b)`从输入流中读取一定数量的字节，并将其存储在缓冲区数组b 中。

`void close( )`关闭此输入流并释放与该流关联的所有系统资源。

#### FileInputStream类

`java.io.FileInputStream extends Inputstream`
`FileInputStream`:文件字节输入流
作用:把硬盘文件中的数据,读取到内存中使用
构造方法:
`FileInputstream( String name)`

`FileInputstream( File file)`
参数:读取文件的数据源
string name:文件的路径

File file:文件
构造方法的作用:
1.会创建一个FileInputstream对象
2.会把FileInputstream对象指定构造方法中要读取的文件

#### 读取字节数据

步骤：

1.创建FileInputstream对象,构造方法中绑定要读取的数据源

2.使用FileInputstream对象中的方法read,读取文件
3.释放资源

> 发现以上读取文件是一个重复的过程，所以可以使用循环优化
>
> 不知道文件中有多少个字节，使用while循环
>
> while循环结束条件,读取到-1的时候结束
>
> 布尔表达式(Len = fis.read())!=-1
> 1.fis.read():读取一个字节
> 2.Len = fis.read():把读取到的字节赋值给变量Len
>
> 3.(Len = fis.read( ) )!=-1:判断变量Len是否不等于-1

#### 一次读取一个字节的原理

文件中有个隐藏的结束标记，而read方法执行后指针会移动，当移动到了结束的标记，就会让虚拟机返回结束的标记

#### 一次读取多个字节的原理

`int read(byte[] b)`从输入流中读取一定数量的字节，并将其存储在缓冲区数组b 中。

> 1.方法的参数byte[]的作用?
> 起到缓冲作用,存储每次读取到的多个字节
> 数组的长度一把定义为1024(1kb)或者1024的整数倍
>
> 2.方法的返回值int是什么?
> 每次读取的有效字节个数

String类的构造方法
`String( byte[] bytes)`:把字节数组转换为字符串
`String(byte[ ] bytes,int offset，int length）`把字节数组的一部分转换为字符串 

offset :数组的开始索引    length:转换的字节个数

![](https://i.bmp.ovh/imgs/2022/01/74be6232dd3bc0d1.png)

#### 使用字节流读取中文的问题

当使用字节流读取文本文件时，可能会有一个小问题。就是遇到中文字符时，可能不会显示完整的字符，那是因为一个中文字符可能占用多个字节存储。所以Java提供一些字符流类，以字符为单位读写数据，专门用于处理文本文件。

1个中文
GBK:占用两个字节       UTF-8:占用3个字节

#### 练习

复制文件的案例

## 字符流

### 字符输入流（Reader）

`java.io.Reader:`字符输入流,是字符输入流的最顶层的父类,定义了一些共性的成员方法,是一个抽象类

共性的成员方法:
`int read()`读取单个字符并返回。
`int read(char[] cbuf)`一次读取多个字符,将字符读入数组。

`void close()`关闭该流并释放与之关联的所有资源。
`java.io.FileReader extends InputstreamReader extends ReaderFiLeReader`:文件字符输入流
作用:把硬盘文件中的数据以字符的方式读取到内存中
构造方法:
`FileReader( String fileName)`

`FileReader(File file)`
参数:读取文件的数据源
string fiLeName:文件的路径

File file:一个文件

FiLeReader构造方法的作用:
1.创建一个FileReader对象
2.会把FileReader对象指向要读取的文件

### 读取字符数据

字符输入流的使用步骤:
1.创建FileReader对象,构造方法中绑定要读取的数据源

2.使用FileReader对象中的方法readi读取文件
3.释放资源

String类的两个构造方法

`String(char[ ] value)`把字符数组转换为字符串    (读取一个字符)
`String(char[] value,int offset，int count）`把字符数组的一部分转换为字  符串       （读取多个字符）   offset数组的开始索引    count转换的个数

### 字符输出流（Writer）

java.io.writer :字符输出流,是所有字符输出流的最顶层的父类,是一个抽象类共性的成员方法:
- `void write(int c)`写入单个字符。

- `void write( char[] cbuf)`写入字符数组。

- `abstract void write(char[ ] cbuf，int off， int len)`写入字符数组的某一部分, off数组的开始索引，len写的字符个数。

- `void write(String str)`写入字符串。

- `void write(String str, int off, int len)`写入字符串的某一部分, off字符串的开始索引, Len写的字符个数。

- ` void flush()`刷新该流的缓冲。

- `void close()`关闭此流，但要先刷新它。

  

  java.io.Filewriter extends OutputStreamwriter extends Writer

  Filewriter:文件字符输出流
  作用:把内存中字符数据写入到文件中

#### 字符输出流的使用步骤(重点)

1.创建Filelwriter对象,构造方法中绑定要写入数据的目的地
2.使用Filewriter中的方法write,把数据写入到内存缓冲区中(字符转换为字节的过程)

3.使用Filewriter中的方法flush,把内存缓冲区中的数据，刷新到文件中
4.释放资源(会先把内存缓冲区中的数据刷新到文件中)

#### flush和close方法的区别

- close:先刷新缓冲区，然后通知系统释放资源。流对象不可以再被使用了

- flush :刷新缓冲区，流对象可以继续使用。

  

### 字符输出流的续写和换行（与字节一样）

续写,追加写:使用两个参数的构造方法
`Filelriter( string fileName, boolean append)`

`Filelriter(File file, boolean append )`
参数:
string fileName, File file:写入数据的目的地
boolean append :续写开关

true:不会创建新的文件覆盖源文件,可以续写;
false:创建新的文件覆盖源文件
换行:换行符号
windows : \r\n

linux:/n
mac : /r

### TryCatch异常处理

#### 之前

```java
FileWriter fw=null;
        try {
             fw=new FileWriter("e:\\txt\\e.txt",true);//这行代码如果正常运行 就可以赋值
            //如果出现异常 就不会赋值  下面的fw=null 不能调用方法 报错
            for (int i = 0; i < 10; i++) {
                fw.write("helloWorld"+i+"\r\n");
            }
//            fw.close();上面的代码出现异常IOException 方法体中不会继续执行
        }catch (IOException e){
            System.out.println(e);
        }finally {
            if (fw!=null)
            try {
                fw.close();//有了初始值才能调用方法 所以赋值null
            } catch (IOException e) {
                e.printStackTrace();
            }
        }
```

//发现太麻烦

#### JDK7新特性

在try的后边可以增加一个(),在括号中可以定义流对象那么这个流对象的作用域就在try中有效
try中的代码执行完毕,会**自动**把流对象释放,不用写finally

 格式:
try(定义流对象;定义流对象....){
可能会产出异常的代码
}catch(异常类变量变量名){
异常的处理逻辑
}

#### JDk9新特性

try的前边可以定义流对象
在try后边的()中可以直接引入流对象的名称(变量名)
在try代码执行完毕之后,流对象也可以释放掉,不用写finally

> 格式:
> A a = new A();B b = new B();
>
> try(a, b){
> 可能会产出异常的代码
>
> }catch(异常类变量变量名){
> 异常的处理逻辑
> }

# Porperties集合

java.util.Properties集合extends Hashtable<k,v> implements Map<k,v>

Properties类表示了一个持久的属性集。Properties可保存在流中或从流中加载。**Properties集合是一个唯—和IO流相结合的集合**

- 可以使用Properties集合中的方法store,把集合中的临时数据,持久化写入到硬盘中

- 存储可以使用Properties集合中的方法load,把硬盘中保存的文件(键值对),读取到集合中使用属性列表中每个键及其对应值都是一个字符串。

  

使用Propertise集合存储数据，遍历取出Propertise集合中的数据

Propertise集合是一个双列集合，key和value默认都为字符串

Properties集合有一些操作字符串的特有方法
`object setProperty(String key, String value）`调用 Hashtable的方法 put。
`String getProperty (String key）`通过key找到value值,此方法相当于Map集合中的get(key)方法
`Set<String> stringPropertyNames()`返回此属性列表中的键集，其中该键及其对应值是字符串,此方法相当于Map集合中的keySet方法

## Properties中的方法store

可以使用Properties集合中的方法store,把集合中的临时数据,持久化写入到硬盘中存储

`void store( OutputStream out, String comments)`
`void store(Writer writer,String comments)`

参数:
Outputstream out:字节输出流,不能写入中文

Writer writer:字符输出流,可以写中文
String comments :注释,用来解释说明保存的文件是做什么用的
不能使用中文,会产生乱码，认是unicode编码
一般使用" "空字符串
使用步骤:
1.创建Properties集合对象,添加数据
2.创建字节输出流/字符输出流对象,构造方法中绑定要输出的目的地
3.使用Properties集合中的方法store,把集合中的临时数据,持久化写入到硬盘中存储4.释放资源

## Properties中的方法load

可以使用Properties集合中的方法load,把硬盘中保存的文件(键值对),读取到集合中使用

`void load ( InputStream inStream)`
`void Load ( Reader reader)`
参数:
InputStream inStream :字节输入流，不能读取含有中文的键值对

Reader reader:字符输入流,能读取含有中文的键值对
使用步骤:
1.创建Properties集合对象
2.使用Properties集合对象中的方法load读取保存键值对的文件

3.遍历Properties集合
注意:
1.存储键值对的文件中,键与值默认的连接符号可以使用=,空格(其他符号)

2.存储键值对的文件中，可以使用#进行注释,被注释的键值对不会再被读取

3.存储键值对的文件中,键与值默认都是字符串,不用再加引号

```java
 Properties pt=new Properties();
        pt.load(new FileReader("10IOAndProperties\\\\prop.txt"));
        Set<String> set = pt.stringPropertyNames();
        for(String key:set){
            String value = pt.getProperty(key);
            System.out.println(key+"="+value);
```

# 缓冲流

## 字节缓冲输出流

java.io.BufferedOutputStream extends OutputStream

Bufferedoutputstream:字节缓冲输出流
继承自父类的共性成员方法:

- public void close()∶关闭此输出流并释放与此流相关联的任何系统资源。
- public void flush():刷新此输出流并强制任何缓冲的输出字节被写出。
- public void write(byte[] b):将b.length字节从指定的字节数组写入此输出流。
- public void write(byte[] b， int off， int len):从指定的字节数组写入len字节，从偏移量off开始输出到此输出流。
-  public abstract void write(int b):将指定的字节输出流。

构造方法:
BufferedOutputStream(OutputStream out)创建一个新的缓冲输出流，以将数据写入指定的底层输出流。
BufferedOutputStream(OutputStream out，int size)创建一个新的缓冲输出流，以将具有指定缓冲区大小的数据写入指定的底层输出流。

参数:
OutputStream out:字节输出流
我们可以传递FileOutputStream , 缓冲流会给FileOutputStream增加一个缓冲区,提高FileOutputStream的写入效率

int size:指定缓冲流内部缓冲区的大小,不指定默认

使用步骤(重点)
1.创建FileoutputStream对象,构造方法中绑定要输出的目的地
2.创建BufferedOutputStream对象,构造方法中传递FileoutputStream对象对象
,提高FiLeoutputstream对象效率
3.使用BufferedoutputStream对象中的方法write,把数据写入到内部缓冲区中
4.使用BufferedoutputStream对象中的方法flush,把内部缓冲区中的数据,刷新到文件中

5.释放资源(会先调用flush方法刷新数据,第4步可以省略）

## 字节缓冲输入流

java.io.BufferedInputStream extends Inputstream

BufferedInputstream:字节缓冲输入流
继承自父类的成员方法:

- int read()从输入流中读取数据的下一个字节。
- int read(byte[ ] b）从输入流中读取一定数量的字节，并将其存储在缓冲区数组b中。
- void close()关闭此输入流并释放与该流关联的所有系统资源。


构造方法:

- BufferedInputStream(InputStream in)创建一个BufferedInputStream并保存其参数，即输入流 in,以便将来使用。
- BufferedInputStream(InputStream in，int size)创建具有指定缓冲区大小的 BufferedInputstreom并保存其参数，即输入流

参数:
Inputstream in:字节输入流
我们可以传递FileInputStream,冲流会给FileInputStream增加一个缓冲区,提高FileInputStream的写入效率

int size:指定缓冲流内部缓冲区的大小,不指定默认

使用步骤(重点):
1.创建FileInputstream对象,构造方法中绑定要读取的数据源
2.创建BufferedInputStream对象，构造方法中传递FileInputStream对象，提高FiLeInputStream对象的读取效率

3.使用BufferedInputStream对象中的方法read,读取文件
4.释放资源

## 字符缓冲输出流

java.io.Bufferedwriter extends writerBufferedwriter:字符缓冲输出流
继承自父类的共性成员方法:
- void write(int c)写入单个字符。

- void write( char[] cbuf)写入字符数组。

- abstract void write(char[] cbuf，int off，int len)写入字符数组的某一部分, off数组的开始索引,len写的字符个数。- void write( String str)写入字符串。

- void write( String str，int off，int len)写入字符串的某一部分, off字符串的开始索引, len写的字符个数。

- void flush()刷新该流的缓冲。

- void close()关闭此流,但要先刷新它。

  构造方法:

  - Bufferedwriter(writer out）创建一个使用黑认大小输出缓冲区的缓冲字符输出流。
  - Bufferedwriter(writer out, int sz)创建一个使用给定大小输出缓冲区的新缓冲字符输出流。

  参数:
  writer out:字符输出流
  我们可以传递FileWriter ,缓冲流会给FileWriter增加一个缓冲区,提高FileWriter的写入效率

  int sz:指定缓冲区的大小,不写默认大小

<font color=red>特有的成员方法</font>:
`void newLine()`写入一个行分隔符。会根据不同的操作系统,获取不同的行分隔符换行

换行符号
windows : /r/n

linux:/ n
mac:/r

使用步骤:
1.创建字符缓冲输出流对象,构造方法中传递字符输出流
2.调用字符缓冲输出流中的方法write,把数据写入到内存缓冲区中
3.调用字符缓冲输出流中的方法flush,把内存缓冲区中的数据,刷新到文件中

4.释放资源

## 字符缓冲输入流

java.io.BufferedReader extends Reader

继承自父类的共性成员方法:

- int read()读取单个字符并返回。
- int read( char[] cbuf)一次读取多个字符,将字符读入数组。void close()关闭该流并释放与之关联的所有资源。

构造方法:

- BufferedReader(Reader in)创建一个使用黑默认大小输入缓冲区的缓冲字符输入流。
- BufferedReader(Reader in, int sz)创建一个使用指定大小输入缓冲区的缓冲字符输入流。

参数:
Reader in:字符输入流
我们可以传递FileReader ,缓冲流会给FileReader增加一个缓冲区,提高FiLeReader的读取效率
<font color=red>特有的成员方法</font>:
string readLine()读取一个文本行。读取一行数据
行的终止符号:通过下列字符之一即可认为某行已终止:换行('\n')、回车('\r')或回车后直接跟着换行(\r\n)。

返回值:
包含该行内容的字符串，不包含任何行终止符，如果已到达流末尾，则返回null

使用步骤:
1.创建字符缓冲输入流对象,构造方法中传递字符输入流
2.使用字符缓冲输入流对象中的方法read/readline读取文本

3.释放资源

## 练习：对文本进行排序



# 转换流(ReverseStream)

## 字符编码

编码:字符(能看懂的)--字节(看不懂的)
解码:字节(看不懂的)-->字符(能看懂的)

## 字符集

- ASCII字符集  

ASCII（American Standard Code for Information Interchange，美国信息交换标准代码）是基于拉丁 字母的一套电脑编码系统，用于显示现代英语，主要包括控制字符（回车键、退格、换行键等）和可显 示字符（英文大小写字符、阿拉伯数字和西文符号）。 基本的ASCII字符集，使用7位（bits）表示一个字符，共128字符。ASCII的扩展字符集使用8位（bits） 表示一个字符，共256字符，方便支持欧洲常用字符。

- GBK（windows默认字符编码）

最常用的中文码表。是在GB2312标准基础上的扩展规范，使用了双字节编码方案，共收录了 21003个汉字，完全兼容GB2312标准，同时支持繁体汉字以及日韩汉字等。

- UTF-8编码

可以用来表示Unicode标准中任何字符，它是电子邮件、网页及其他存储或传送文字的应用 中，优先采用的编码。互联网工程工作小组（IETF）要求所有互联网协议都必须支持UTF-8编码。所以， 我们开发Web应用，也要使用UTF-8编码。它使用一至四个字节为每个字符编码，

编码规则

1. 128个US-ASCII字符，只需一个字节编码。

2. 拉丁文等字符，需要二个字节编码。 
3. 大部分常用字（含中文），使用三个字节编码。
4.  其他极少使用的Unicode辅助字符，使用四字节编码。

## 原理

![](https://i.bmp.ovh/imgs/2022/01/4f651eb02df42936.png)

## OutputStreamWriter

`java.io.OutputStreamWriter extends Writer`
OutputStreamWriter:是字符流通向字节流的桥梁:可使用指定的  charset  将要写入流中的字符编码成字节。(编码:把能看懂的变成看不懂)

继续自父类的共性成员方法:
- void write(int c)写入单个字符。
- void write(char[]cbuf)写入字符数组。
- abstract void write(char[] cbuf，int off, int len)写入字符数组的某一部分, off数组的开始索引,len写的字符个数。
- void write(String str)写入字符串。
- void write(String str，int off， int len)写入字符串的某一部分,off字符串的开始索引,len写的字符个数。
-  void flush()刷新该流的缓冲。
- void close()关闭此流，但要先刷新它。

构造方法:

- OutputStreamwriter(OutputStream out)创建使用黑认字符编码的OutputStreamiriter。
- OutputStreamWriter(OutputStream out,String charsetName)创建使用指定字符集的 OutputStreamWriter。

参数:
outputStream out:字节输出流,可以用来写转换之后的字节到文件中
string charsetName :指定的编码表名称,不区分大小写,可以是utf-8/UTF-8,gbk/GBK] . ..不指定默认使用UTF-8

使用步骤:
1.创建outputStreamlriter对象,构造方法中传递字节输出流和指定的编码表名称
2.使用outputstreamwriter对象中的方法write,把字符转换为字节存储缓冲区中(编码)
3.使用outputStreamwriter对象中的方法flush,把内存缓冲区中的字节刷新到文件中(使用字节流写字节的过程)

4.释放资源

## InputStreamReader

java.io.InputstreamReader extends Reader
InputStreamReader:是字节流通向字符流的桥梁:它使用指定的charset 读取字节并将其解码为字符。(解码:把看不懂的变成能看懂的)

继承自父类的共性成员方法:

- int read()读取单个字符并返回。
- nt read ( char[] cbuf)一次读取多个字符,将字符读入数组。
- void close()关闭该流并释放与之关联的所有资源。

构造方法:

- InputStreamReader(InputStream in)创建一个使用黑认字符集的InputStreamReadero
- InputStreamReader(InputStream in，String charsetName)创建使用指定字符集的InputStreamReader。

参数:
Inputstream in:字节输入流,用来读取文件中保存的字节
string charsetName:指定的编码表名称,不区分大小写,可以是utf-8/UTF
-8,gbk/GBK, ...不指定默认使用UTF-8
使用步骤:
1.创建InputstreamReader对象,构造方法中传递字节输入流和指定的编码表名称

2.使用InputstreamReader对象中的方法read读取文件
3.释放资源
注意事项:
构造方法中指定的编码表名称要和文件的编码相同,否则会发生乱码

## 练习：转换文件编码

将GBK编码的文本文件,转换为UTF-8编码的文本文件。

# 序列化流

## 概述

![](https://i.bmp.ovh/imgs/2022/01/5d6bcec83e937819.png)

Person p = new Person("小美女".18);
把对象以流的方式,写入到文件中保存,叫写对象,也叫对象的序列化对象中包含的不仅仅是字符,使用字节流
ObjectOutputStream:对象的序列化流

把文件中保存的对象,以流的方式读取出来叫做读对象,也叫对象的反序列化读取的文件保存的都是字节,使用字节流
ObjectInputStream:对象的反序列化流

## 对象的序列化流

java.io.0bjectOutputStream extends OutputStream

ObjectOutputstream:对象的序列化流
作用:把对象以流的方式写入到文件中保存
构造方法:
ObjectOutputStream(OutputStream out)创建写入指定OutputStream 的 ObjectOutputStream

参数:
OutputStream out:字节输出流
特有的成员方法:
void writeObject(Object obj）将指定的对象写入ObjectOutputStream 
使用步骤:
1.创建ObjectOutputStream对象,构造方法中传递字节输出流
2.使用ObjectOutputStream对象中的方法writeObject,把对象写入到文件中

3.释放资源

序列化和反序列化的时候,会抛出`NotSerializableException`没有序列化异常
类通过实现 java.io.Serializable接口以启用其序列化功能。未实现此接口的类将无法使其任何状态序列化或反序列化

Serializable接口也叫标记型接口
要进行序列化和反序列化的类必须实现serializable接口,就会给类添加一个标记当我们进行序列化和反序列化的时候,就会检测类上是否有这个标记
有:就可以序列化和反序列化
没有:就会抛出NotserializabLeException异常

去市场买肉-->肉上有一个蓝色章(检测合格)-->放心购买-->买回来怎么吃随意

## 反序列化流

java.io.ObjectInputStream extends InputStream

ObjectInputStream:对象的反序列化流
作用:把文件中保存的对象,以流的方式读取出来使用

构造方法:
ObjectInputStream(InputStream in）创建从指定InputStream 读取的ObjectInputStream。

参数:
lnputStream in:字节输入流

特有的成员方法:
object readobject()从ObjectInputStream 读取对象。

使用步骤:
1.创建objectInputstream对象,构造方法中传递字节输入流
2.使用objectInputstream对象中的方法read0bject读取保存对象的文件

3.释放资源
4.使用读取出来的对象(打印)
readobject方法声明抛出了classNotFoundException(class文件找不到异常)当不存在对象的class文件时抛出此异常

反序列化的前提:
1.类必须实现serializable

2.必须存在类对应的class文件

## transien关键字

<font color=red>static关键字</font>:静态关键字
静态优先于非静态加载到内存中(静态优先于对象进入到内存中)被static修饰的成员变量**不能被序列化**的,序列化的都是对象

private static int age;
oos.writeobject(new Person(”小美女",18));

object o = ois.readobject( );
Person{name='小美女',age=0}

<font color=red>transient关键字</font>:瞬态关键字
被transient修饰成员变量,**不能被序列化**

private trgnsient int age;
oos.writeobject( new Person("小美女”,18));

object o = ois.read0bject( );
Person{name='小美女',age=0}

没有static关键字的含义 但是却有static关键字的相同作用

当不想某一成员变量被序列化时 使用transien关键字

## 序列号冲突异常的原理和解决方案

InvalidClassException

问题:
每次修改类的定义,都会给class文件生成一个新的序列号

解决方案:
无论是否对类的定义进行修改,都不重新生成新的序列号，可以手动给类添加一个序列号
格式在Serializable接口规定:
可序列化类可以通过声明名为"serialVersionUID”的字段(该字段必须是静态(static)、最终(final)的long型字段)显式声明其自己的serialVersionUID:
static final long serialVersionUID =42L;常量不能改变

## 练习：序列化集合

1.将存有多个自定义对象的集合序列化操作，保存到list.txt文件中。
2.反序列化list.txt，并遍历集合，打印对象信息。

# 打印流

java.io.PrintStream:打印流
PrintStream为其他输出流添加了功能，使它们能够方便地打印各种数据值表示形式。

PrintStream特点:
1.只负责数据的输出,不负责数据的读取
2.与其他输出流不同，Printstream永远不会抛出IOException

3.有特有的方法, print,println
void print(任意类型的值)
void println(任意类型的值并换行)

构造方法:

- Printstream( File file):输出的目的地是一个文件
- Printstream( OutputStream out):输出的目的地是一个字节输出流
- Printstream ( String fileName):输出的目的地是一个文件路径

`PrintStream extends OutputStream`
继承自父类的成员方法:

- public void close():关闭此输出流并释放与此流相关联的任何系统资源
- public void flush():刷新此输出流并强制任何缓冲的输出字节被写出。

- public void write(byte[] b):将b.Length字节从指定的字节数组写入此输出流。
- public void write(byte[ ] b， int off， int len):从指定的字节数组写入len字节，从偏移量off开始输出到此输出流。
- public abstract void write(int b):将指定的字节输出流。

注意：
如果使用继承自父类的write方法写数据,那么查看数据的时候会查询编码表97->a

如果使用自己特有的方法print/println方法写数据,写的数据原样输出97->97

## setOut方法

可以改变输出语句的目的地(打印流的流向)输出语句,默认在控制台输出
使用system.setOut方法改变输出语句的目的地改为参数中传递的打印流的目的地

静态方法

`System.setOut(PrintStream out)`

`static void setOut( PrintStream out)`

重新分配“标准”输出流。
