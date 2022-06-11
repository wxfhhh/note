

[TOC]



#  常用API二



# Object类

## toString方法

java.lang.Object类

类 Object 是类层结构的根(最顶层)类。每个类都使用Object作为超类（父类）。

所有对象（包括数组）都实现这个类的方法。

> 看一个类是否重写了toString方法，直接打印这个类对应对象的名称即可
>
> 如果没有重写toString方法，那么打印的就是对象的地址值（默认）
>
> 如果重写了toString方法，那么就按照重写的方式打印

直接打印对象名字，其实就是调用对象的toString方法 

<!--数组调用toString就是遍历数组 Arrays.toString(数组)-->

## equals方法

  boolean equals(Object obj)指示其他某个对象是否与此对象“相等”。

```java
//源码
public boolean equals(Object obj){
    return this==obj;
} 
```

参数：

​       Object obj：可以传递任意的对象

方法体：

> ==：比较运算符，返回的就是一个布尔值 true false
>
> 基本数据类型：比较的是值
>
> 引用数据类型：比较的是两个对象的地址值
>
> this是谁？哪个对象调用的方法，方法中的this就是那个对象；p1调用的equals方法，所以this就是p1
>
> obj是传递过来的参数p2 
>
> <!--this==obj 就是 p1==P2-->

## equals的重写方法

equals比较的是两个对象的地址值，这样写是没有意义的

所以我们需要重写equals方法，比较两个对象的属性值(name,age)

 对象的属性值一样，则返回 true;否则返回false

> 问题：
>
> 隐含着一个多态
>
> Object obj =one Person(name,age);
>
> 多态的弊端：无法使用子类特有的内容
>
> 所以使用向下转型把Object转换为Person

```java
public boolean equals(Object o) {
        if (this == o) return true;
        if (o == null || getClass() != o.getClass()) return false;
        Person person = (Person) o;
        return age == person.age && Objects.equals(name, person.name);
}
```

## Objects中的equals方法

目的：为了防止空指针异常

```java
 public static boolean equals(Object a, Object b) {
        return (a == b) || (a != null && a.equals(b));
    }
```

a==null就会返回false

# Date类

java.util.Date:表示日期和时间的类

类 Date 表示特定的瞬间，精确到毫秒。

毫秒：千分之一秒 1000毫秒=1秒

特定的瞬间：一个时间点，一刹那时间

> 2088-08-08 09：55：33：333
>
> 2088-08-08 09：55：33：334
>
> 2088-08-08 09：55：33：335
>
> ...

毫秒值的作用：可以对时间和日期进行计算

2099-01-03到2088-01-01 中间一共有多少天

可以日期转换为毫秒进行计算，计算完毕，在把毫秒换为日期

## 把日期转换为毫秒

当前的日期：2088-01-01

时间原点(0毫秒的点)：1970年1月1日00:00:00（英国格林威治）

就是计算当前日期到时间原点之间一共经历了多少毫秒（）

注意：中国属于东八区，会把时间增加到8个小时

1970年1月1日08:00:00

```java
  Date date=new Date();
        System.out.println(date);
        //空参数的构造方法：获取当前的时间
```



## 把毫秒换成日期:

1 天=24 *60 *60=86400秒=86400000毫秒

```java
 Date date1=new Date(12222222223L);
        System.out.println(date1);
//        有参数的构造方法 ：传递毫秒值 把毫秒值转换为Date
```

```java
public class Demo01Date {
    public static void main(String[] args) {
        Date date=new Date();
        System.out.println(date);
        //空参数的构造方法：获取当前的时间
        Date date1=new Date(12222222223L);
        System.out.println(date1);
//        有参数的构造方法 ：传递毫秒值 把毫秒值转换为Date
        GetTime();

    }
    public static void GetTime(){
        //Date类的成员方法
        //long getTime() 把日期转换为毫秒
        //(相当于System.currentTimeMillis())
        //返回自 1970年1月1日00:00:00 GMT 
        //以来此Date 对象表示的毫秒数
        Date date=new Date();
        long time = date.getTime();
        System.out.println(time);

    }
}

```

## DateFormat类 SimpleDateFormat类

java.text.DateForMat:是日期/时间格式化子类的抽象类

> 作用：
>
>   格式化（也就是日期->文本） 解析(文本->日期)

#### 日期—>文本 （format方法）

使用步骤：

1. 创建SimpleDateFormat对象，构造方法中传递指定模式
2. 调用SimpleDateFormat对象中的format方法，按照指定模式把Date日期转换为符合模式的字符串

#### 文本—>日期（parse方法）

1. 创建SimpleDateFormat对象，构造方法中传递指定模式
2. 调用SimpleDateFormat对象中的parse方法，把符合构造方法中的字符串解析为Date日期

```java

```



##### 注意事项

parse方法中声明了一个异常 叫ParseException

如果字符串和构造方法中的模式不一样 那么程序就会出现此异常

处理：

1. ​       用throw继续声明抛出这个异常
2. try...catch自己处理这个异常



### 成员方法

String format(Date date)  按照指定的格式，把Date日期，格式化为符合模式的字符串

Date parse(String source) 把符合模式的字符串 解析为Date日期

<!--注意 DateFormat类是一个抽象类，无法直接创建对象使用，可以使用DateFormat的子类 SimpleDateformat-->

### 构造方法

SimpleDateFormat(string pattern) 用给定的模式和默认语言环境的日期格式符号构造   SimpleDAteFormat

创建对象时使用构造方法

参数：

​     String patter 指定的模式

> 模式： 区分大小写的
>
> y  年
>
> M 月
>
> d 日
>
> H 时
>
> m 分
>
> s 秒



```java
public static void main(String[] args) throws ParseException {
        method();

    }
    public static void method() throws ParseException {
        SimpleDateFormat dateFormat=new SimpleDateFormat(
                "yyyy-MM-dd HH:mm:ss");
        Date date=new Date();
        System.out.println(dateFormat.format(date));
        SimpleDateFormat dateParse=new SimpleDateFormat(
                "yyyy-MM-dd HH:mm:ss");
        Date date1=dateParse.parse("2021-11-27 23:50:30");
        System.out.println(date1);
    }
```

### 练习

计算一个人一共出生了多少天

```java
Scanner sca=new Scanner(System.in);
        System.out.println("请输入你的出生年月 格式为 yyyy-MM-dd");
        String birthdayDateString = sca.next();
        SimpleDateFormat DateFormat=new SimpleDateFormat(
                "yyyy-MM-dd");
        Date date1=DateFormat.parse(birthdayDateString);
        long time1 = date1.getTime();
        long time2=new Date().getTime();
        long result=time2-time1;

        System.out.println(result/86400000);
```

# Calendar类 日历类

概述： Calendar类是一个抽象类，里面提供了很多操作日历字段的方法(YEAR、MONTH、DAY_OF_MONTH、HOUR)

Calendar类无法直接创建对象来使用，里边有一个静态方法叫getInstance(),该方法返回了Calendar类的子类对象 static Calendar getInstance( ) 使用默认时区和语言环境获得一个日历。

```java
public static void main(String[] args){
    Calendar c =Calendar.getInstance();//多态
    System.out.println(c);//属性值
}
```

## Calendar类的常用成员方法

```java
public int get(in field)
    //返回给定日历字段的值
public void set(int field,int value)
    //将给定的日历字段设置为给定值
public abstract void add(int field,int amount)
    //根据日历的规则，为给定的日历字段添加或减去指定的时间量
public Date getTime()
    //返回一个表示此Calendar时间值(从历元到现在的毫秒偏移量)的DAte对象。把日历对象转换为日期对象
```

（add）参数：

​     int field ：传递指定的日历字段(YEAR,MONTH)

​     int amount:增加或减少的量

​          正数：增加

​          负数：减少 

### 成员方法的参数

int field:日历类的字段，可以使用Calendar类的静态成员变量获取

```java
public static final int YEAR = 1;年
public static final int NONTH = 2;月
public static final int DATE = 5;月中的某一天
public static final int DAY_OF_MONTH = 5;月中的某一天

public static final int HOUR = 10;时
public static final int MINUTE = 12;分
public static final int SECOND = 13;秒
```

# System类

## 几个成员方法

```java
public static long currentTimeMillis()
    //返回以毫秒为单位的当前时间
public static void arraycopy(Object src,int srcPos,Object dest,int destPos,int length)
    //将数组中指定的数据拷贝到另一个数组中
```

> src - 源数组。
> srcPos - 源数组中的起始位置。
> dest - 目标数组。
> destPos - 目标数据中的起始位置。
> length - 要复制的数组元素的数量。 

public static long currentTimeMillis( )

可以用来测试程序的效率

练习：

验证for循环打印1-9999所需要的时间(毫秒)

### 练习

test1：验证for循环打印1-9999所需要的时间(毫秒)

```java
long l = System.currentTimeMillis();
        for (int i = 1; i <=9999 ; i++) {
            System.out.println(i);
        }
        long l1 = System.currentTimeMillis();
        System.out.println(l1-l);
```

test2：将src数组中前个元素,复制到dest数组的前3个位置上
复制元素前: srlc数组元素[1,2,3,4,5]，dest数组元素[6,7,8,9,10]

复制元素后: src数组元素[1,2,3,4,5]，dest数组元素[1,2,3,9,10]

```java
 int[] src ={1,2,3,4,5};
        int[] dest={6,7,8,9,10};
        System.out.println(Arrays.toString(src));
        System.out.println(Arrays.toString(dest));
        System.arraycopy(src,0,dest,0,3);
        System.out.println(Arrays.toString(src));
        System.out.println(Arrays.toString(dest));
```

# StringBuilder类

## 与String类的区别

java.lang.StringBuilder

> String类
>
> 字符串是常量;它们的值在创建之后不可改变。
>
> 字符串的底层是一个被final修饰的数组，不能改变，是一个常量
>
> ```java
> private final byte[] value;
> ```
>
> 进行字符串的相加，内存中就会有多个字符串，占用空间多，效率低下
>
> String s="a"+"b"+"c"="abc";
>
> 一共创建了5个字符串  "a" "b" "c" "ab" "abc"
>
>    占用空间多，效率低下



> StringBuilder类
>
> 字符串缓冲区，可以提高字符串的操作效率(<font color=red>看成一个可以变化的字符串</font>)
>
> 底层也是一个数组，但是没有被final修饰，可以改变长度
>
> ```java
> byte[] value=new byte[16];
> ```
>
> StringBuilder在内存中始终是一个数组，占用空间少，效率高
>
> 如果超出了StringBuilder的容量，会自动的扩容

## 构造方法

```java
public StringBuilder()
    //构建一个空的StringBuilder容器
    //不为null e
public StringBuilder(String str)
    //构造一个StringBuilder容器 并将字符串添加进去
```

## 成员方法

```java
public StringBuilder append(...)
    //添加任意类型数据的字符串形式，并返回当前对象自身。
    //参数：
    //可以是任意的数据类型
public String toString()
    //将当前StringBuilder对象转换为String对象。

```

注意：使用append方法往StringBuider中添加数据 返回的是this（本类的对象）

```java
StringBuilder sbd1=new StringBuilder();
        StringBuilder sbd2=sbd1.append(123);
        System.out.println(sbd1);
        System.out.println(sbd2);
        System.out.println(sbd1==sbd2);
//==在引用数据类型中比较的是地址值
// 如果地址值一样，则说明这是两个相同的对象
```

### 链式编程

```java
 StringBuilder sbd1=new StringBuilder();
sbd1.append("abc").append("qwe");
        //链式编程
        System.out.println(sbd1);
```



## StringBuilder和String之间的相互转换

1.String->StringBuilder ：使用StringBuilder的构造方法

StringBuilder(String str) 

2.StringBuilder->String 可以使用StringBuilder中的toString方法

public String toString( ) 

```java
 //String->StringBuilder
        //使用stringBuilder的构造方法
        StringBuilder sbu1=new StringBuilder("abc");
        //StringBuilder->String
        //使用StringBuilder的toString方法
        String string = sbu1.toString().substring(0,1);
//        变成String 就可以调用String类中的方法
        System.out.println(string);
```

# 包装类(packaging)

> 基本数据类型的数据，使用起来非常的方便，但是没有对应的方法来操作这些数据，所以我们可以使用一个类，把基本数据类型包装起来，这个类叫做包装类 在包装类中可以定义一些方法，用来操作基本类型的数据

## 装箱与拆箱

### 装箱

把基本类型的数据，包装到包装类中（基本类型的数据->包装类）

1. 构造方法

   ```java
   Integer(int value)
       //构造一个新分配的Integer对象，它表示指定的Integer值
   Integer(String s)
       //构造一个新分配的Integer对象，它表示String参数所指定的int值
   //注意传递的必须是基本数据类型的字符串，否则会抛出异常 如”a“
   ```

   

2. 静态方法

   ```java
   static Integer valueOf(int i)
       //返回一个表示特定的int值的Integer实例
   static Integer valueOf(String s)
       //返回保存指定的String的值的Integer对象拆箱
   ```


### 拆箱

在包装类中取出基本类型的数据（包装类->基本类型的数据）

成员方法

```java
//int intValue() 以 int 类型返回该Integer的值
    int i=in1.intValue();
    System.out.println(i);
```

## 自动装箱和自动拆箱

自动装箱：

直接把int类型的整数赋值给包装类

```java
//Interger in =1;
//就相当于
//Integer in=new Integer(1);
```

自动拆箱：

in 是包装类，无法直接参与运算，可以自动转换为基本类型的数据，再参与计算

```java
 //int intValue() 
   //       以 int 类型返回该 Integer 的值。 
Integer in=1;
in + 2;
//相当于 in.intValue()+3=3;
in = in + 2;
//就相当于 in = new Integer(3) 自动装箱
in = in + 2;
System.out.println(in);
```

## 基本类型与字符串之间的转换

### 基本类型——>字符串

1. 基本类型数据的值+" "  ( 最简单的方法 工作中常用)

2. 使用包装类中的静态方法

   ```jaVa
   static String toString(int i)
      // 返回一个表示指定整数的String对象
   ```

   

3. 使用String类中的静态方法

```java
static String valueOf(int i)
    返回int参数的字符串表示形式。
```

### 字符串——>基本类型

 使用包装类的静态方法 parseXX("字符串")

```java
//Integer类 static int parseInt(String s)
 //Double类  static double parseDouble(String s)
```

