[TOC]

# **API文档**

查询 点显示 索引 

看包路径 看构造方法 看方法摘要

导包指名包路径   创建指名构造方法   方法摘要是使用

# Scanner类

- Scanner类的功能：可以实现键盘输入数据到程序当中。

- 引用类型的一般使用步骤：

  1. 导包：import 包路径.类名称;

     如果需要使用的目标类，和当前类位于同一个包下，则可以省略导包语句不写。只有java.lang包下的内容不需要导包，其他的包都需要import语句。

  2. 创建：类名称 对象名=new 类名称;

  3. 使用：对象名.成员方法名()

  ```java
  （导包省略）
      Scanner sca =new Scanner(System.in);//创建，System.in表示从键盘进行输入
      int num=sca.nextInt;//规定输入数字的类型 获取输入的数字
      System.out.printnl(num);
      String str=sca.next;//获取输入的字符串
     System.out.printnl(str);
  ```

  

# 匿名对象

就是只有右边的对象名和名称，没有等号左边的对象名和名称

```java
 new Person().name="高圆圆";//匿名对象
 Person one = new Person();//非匿名对象
 one.name="高圆圆";
 one.showName();//我叫高圆圆
```

## 注意事项：

匿名对象只能使用唯一的一次，下次再用不得不再创建一个新对象。

![image-20210928191202691](C:\Users\ASUS\AppData\Roaming\Typora\typora-user-images\image-20210928191202691.png)

发现showName的时候出现了null，说明匿名对象只能用一次，而表示null的原因是重新建立了一个对象（即又出现了一个new）

使用建议：如果确定有一个对象只需要使用唯一的一次，就可以使用匿名对象。

匿名对象没有名称，使用时在new 类名称( )后点啥啥。

```java
Scanner sca=new Scanner(System.in);
int a =sca.nextInt;//普通的使用
int a =new Scanner.nextInt;//匿名对象d
```

## 匿名对象作为参数和返回值

作为参数

![image-20210928192631029](C:\Users\ASUS\AppData\Roaming\Typora\typora-user-images\image-20210928192631029.png)

技巧： int num =sc.nextInt( );这一行输入sc.nextInt( )后点alt键加回车可以直接打完整行。

## 作为返回值

![image-20210928193312138](C:\Users\ASUS\AppData\Roaming\Typora\typora-user-images\image-20210928193312138.png)

第一行相当于 Scanner sc =new Scanner(System.in);

返回什么，就将要返回的内容传递给调用处。

# Random类

概念：获取一个随机数字

![image-20210928194030930](C:\Users\ASUS\AppData\Roaming\Typora\typora-user-images\image-20210928194030930.png)

获取一个随机的int数字（参数代表了范围，左开右闭区间）：int num =r.nextInt(3);代表的就是范围为[0,3)也就是0~2.

![image-20210928194649240](C:\Users\ASUS\AppData\Roaming\Typora\typora-user-images\image-20210928194649240.png)

## 练习

1.生成1到n之间的随机数。

（整体加一就好）<!--我最初的想法是if（num！=0）System.out.prinln(r);-->

2.猜数字小游戏。

# Arraylist集合

## 对象数组

定义一个数组，用来存储若干个对象。

![](https://i.bmp.ovh/imgs/2021/11/6ca591692cb97ef4.png)

缺点：一旦创建，数组的长度就不可改变

当不知道要存储多少个对象时 数组用起来就不太方便

ArrayList集合

![](https://i.bmp.ovh/imgs/2021/11/b7a5bb309bbbe40c.png)

自动装箱：基本类型--> 包装类型

自动拆箱：包装类型-->基本类型

常用方法：

![](https://i.bmp.ovh/imgs/2021/11/b38ec6a751fa1f3e.png)

用for循环来遍历一个集合

创建的集合对象名.fori (快捷方式)

```java
  ArrayList<Integet> list =new ArrayList<>;
  list.add(1);
  list.add(2);
  list.add(3);
for(int i=0;i<list.size();i++){
    System.out.println(list.get(i));
}

```

练习 三个练习

# String类

java.lang.String类代表字符串。

API当中说：java程序中所有的字符串面值，都作为此类的实例实现。

其实就是说：程序当中所有的双引号字符串，都是String类的对象。

字符串的特点:

1. 字符串的内容永不可变。 【重点】
2. 正是因为字符串不可改变，所以字符串是可以共享的。
3. 字符串效果上是相当于char[ ]字符数组，但底层原理是byet[ ]字节数组。

## 创建字符串的常见3+1种方式

三种构造方法：

```java
public String()://创建一个空白字符串，不含任何内容
public String(char[] array)://根据字符数组创建一个对应的字符串
public String(byte[] array)://根据字节数组创建一个对应的字符串
```

直接创建：String str="aaaa";

## 字符串的常量池

概念：程序中直接写上的双引号字符串，就在字符串的常量池中。

对于基本类型来说，==是进行数值的比较

对于引用类型来说，==是进行【地址值】的比较

```java
 String str=new String();
        char[] array1={'a','b','c'};
        String str1=new String(array1);
        byte[] array2={1,2};
        String str2=new String(array2);
        String str3="abc";
        String str4="abc";
        System.out.println(str1==str3);//false d
        System.out.println(str4==str3);//true
```

![](https://i.bmp.ovh/imgs/2021/11/99d00af12e87c106.png)

## 字符串的比较 相关方法

 字符内容的比较：

注意事项：

1. 任何对象都能用Object进行接收。
2. equals方法具有对称性，也就是a.equals(b)和b.equals(a)效果一样。
3. 如果比较双方一个常量一个变量，推荐把常量字符串写在前面。

两种方法：

```java
public boolean equals(Object obj):
//参数可以是任何对象，只有参数是一个字符串并且内容相同才会给true；
//否则返回false 备注：任何对象都能用Object进行接受
public Boolean equalsIgnoreCase(String str)
    //忽略大小写 进行字符的比较
```



```java
System.out.println("abc".equals(str5));//推荐
System.out.println(str5.equals("abc"));//不推荐：有可能会报错，空指针异常NullPointerException
System.out.printnl(strA.equals(strB));//严格区分大小写
System.out.printnl(strA.equalsIgnoreCase(strB));//忽略大小写
//只限于英文
```

## 字符串的获取常用方法（StringGet）

```java
public int length()
    //获取字符串当中含有的字符个数，拿到字符串长度。
public String concat(String str)
    //将当前字符串和参数字符串拼接成为返回值新的字符串//
public char charAt(int index)
    //获取指定索引位置的单个字符串(索引从0开始)
public int indexOf(String str):
//查找参数字符串在本字符串当中首次出现的索引位置，如果没有返回-1值
public int indexOf(String str, int fromIndex)
    //返回从 fromIndex 位置开始查找指定字符在字符串中第一次出现处的索引，如果此字符串中没有这样的字符，则返回 -1。(包括fromIndex这个位置的字符)
```

## 字符串的转换方法（StringConvert）

```java
public char[] toCharArray()
    //将当前字符串拆分为字符数组作为返回值
public byte[] getBytes()
    //获取当前字符底层的字节数组
public String replace(CharSequence oldString,CharSequence newString );
//将所有出现的老字符串替换成为新的字符串，返回替换之后的结果新字符串
```

## 字符串的截取方法(substring)

```java
public String substring(int index)
    //截取从参数位置一直到字符串末尾，返回新的字符串
public String substring(int begin,int end)
    //截取从begin开始，一直到end结束，中间的字符串
    //备注[begin,end),包含左边 不包含右边。
    y
```

## 字符串的分割方法(StringSplit)

```java
public String[] split(String index)
    //按照参数的规则，将字符串切分为若干个部分
   
```

### 注意事项

split方法的参数其实是一个“正则表达式”

今天要注意：如果按照英文句点“.”进行切分，必须写"\\\\\."(两个反斜杠)

> 为什么呢：因为这个句点"."在正则表达式中有重要含义

## 两个练习

# static静态

## 静态的概述

一旦使用了static关键字，那么这样的<font color=red>内容不再属于自己</font>，而是属于类的，所以凡是本类的对象，都共同享有一份。

> 对于姓名、年龄、学号来说，每个对象都要<font color=red>自己独立的数据</font>
>
> 但是对于所在教室来说，这应该是<font color=red>多个对象共享一分数据</font>才对

## 静态关键字修饰成员变量（StaticField）

代码实现

```java
public class Student {
    private String name;
    private int age;
    private static int id ;
    static int classroom;
    private static int idCount=0 ;



    public Student() {
        this.id = ++idCount;
//   按照运行顺序 先将idCount的值加1 再赋值给id
//   如果是 this.id=idCount++; 

    }

    public Student(String name, int age) {
        this.name = name;
        this.age = age;
        this.id = ++idCount;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public int getAge() {
        return age;
    }

    public void setAge(int age) {
        this.age = age;
    }

    public static int getId() {
        return id;
    }

    public static void setId(int id) {
        Student.id = id;
    }
}
```

## 静态关键字修饰成员方法

如果有了static关键字，那么就不再需要创建对象，直接就能通过类名称来使用它

无论是成员变量还是成员方法。如果有了static，都推荐使用类名称来进行调用。

静态方法： 类名称.静态变量

静态方法： 类名称.静态方法( )

### 注意事项：

1. 静态不能直接访问非静态。

   原因：因为在内存当中是【先】存在的静态内容，【后】有的非静态内容。

2. 静态方法当中不能用this

   原因：this代表当前对象，通过谁调用的方法，谁就是当前对象。

## 静态代码块

```java
public class 类名称{
    static{
        //静态代码块的内容
    }
}
```

特点：当第一次使用本类时，静态代码块执行唯一的一次。

静态内容总是优先于非静态，所以静态代码块比构造方法先执行。

静态代码块的典型用途：

用来一次性地对静态成员变量进行赋值。

# Arrays工具类

java.util.Arrays是一个与数组相关的工具类，里面提供了大量的静态方法，用来实现数组常见的操作。

```java
public static String toString(数组)
    //将参数数组变成字符串（按默认格式：[元素一，元素二，元素三...]）
    //使用格式 Arrays.tostring()
public static void sort
//按照默认升序（从小到大）对数组的元素进行排序
//Arrays.sort
         int[] array1={1,2,3,4};
         System.out.println(Arrays.toString(array1));

        int[] array2={4,5,3,2,7,1};
        Arrays.sort(array2);
        System.out.println(Arrays.toString(array2));
```

## 备注

1. 如果是数值，sort默认按照升序从小到大
2. 如果是字符串，sort默认按照字母升序
3. 如果是自定义的类型，那么这个自定义的类需要有Comparable或者Comparator接口的支持。（今后学习）

## 练习 字符串倒序排列

请使用Arrays相关的API，将一个随机字符串中的所有字符升序排列，并倒序打印。

```java
 String str="sfdsfsfghghhjyj";
        char[] chars = str.toCharArray();
        Arrays.sort(chars);
        System.out.println(Arrays.toString(chars));
        for (int i =  chars.length-1; i >=0; i--) {
            System.out.println(chars[i]);
```

# Math类

包路径：java.lang.Math类是数学相关的工具，里面提供了大量的静态方法，完成与数学相关的操作。

```java
public static double abs(double num)
    //获取绝对值
public static double ceil(double num)
    //向上取整
public static double floor(double num)
    //向下取整
public static long round(double num)
    //四舍五入
    //注意只有四舍五入没有小数点 以上其他都存在小数点
static double pow(double a, double b) 
         / 返回第一个参数的第二个参数次幂的值 
    Math.PI代表近似的圆周率常量(double).
   
```

