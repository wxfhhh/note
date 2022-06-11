[TOC]

# web相关概念回顾

## 1软件架构

1.C/S∶客户端/服务器端2.B/S :浏览器/服务器端

## 2资源分类

1．静态资源∶所有用户访问后，得到的结果都是一样的，称为静态资源.静态资源可以直接被浏览器解析
如: html,css,Javascript
2、动态资源:每个用户访问相同资源后，得到的结果可能不一样。称为动态资源。动态资源被访问后，需要先转换为静态资源，再返回给浏览器.
*如: servlet/jsp,php, asp... .

## 3网络通信三要素

1.IP∶电子设备(计算机)在网络中的唯一标识。
2．端口∶应用程序在计算机中的唯一标识。0~655363．传输协议∶规定了数据传输的规则
1．基础协议︰

tcp:安全协议，三次握手。速度稍慢

udp :不安全协议。速度快

# web服务器软件

web服务器软件︰
服务器:安装了服务器软件的计算机
服务器软件:接收用户的请求，处理请求，做出响应
web服务器软件:接收用户的请求，处理请求，做出响应。
*在web服务器软件中，可以部署web项目，让用户通过浏览器来访问这些项目

web容器

常见的iava相关的web服务器软件∶
`webLogic` : oracle公司，大型的JavaEE服务器，支持所有的JavaEE规范，收费的。`websphere` : IBM公司，大型的JavaEE服务器，支持所有的JavaEE规范，收费的。`JBOSS` : JBOSS公司的，大型的JavaEE服务器，支持所有的JavaEE规范，收费的。
`Tomcat` Apache基金组织，中小型的JavaEE服务器，仅仅支持少量的javaEE规范servlet/jsp。开源的，免费的。
JavaFF :Java语言在企业级开发中使用的技术规范的总和，一共规定了13项大的规范

# Tomcat

Tomcat : web服务器软件
1.下载: http: //tomcat.apache.org/

2．安装∶解压压缩包即可。
*注意:安装目录建议不要有中文和空格

![image-20220512194449544](C:\Users\ASUS\AppData\Roaming\Typora\typora-user-images\image-20220512194449544.png)

3．卸载:删除目录就行了

4.启动∶
bin/ startup.bat ,双击运行该文件即可
*访问∶浏览器输人:http:// localhost:8080 回车访问自己
                                    http://别人的ip:8080   访问别人

启动遇到的问题:

可能遇到的问题:

1. 黑窗口一闪而过︰
   原因:没有正确配置JAVA_HOME环境变量*解决方案︰正确配置JAVA_HOME环境变量
2. 启动报错︰
   1．暴力∶找到占用的端口号，并且找到对应的进程，杀死该进程
   cmd中输入`netstat -ano` 找到8080端口号的PID 再在任务管理器中结束此PID的进程
   2．温柔:修改自身的端口号
   *conf/ server.xml中找到
   *<Connector port="8888" protocol="HTTP/1.1"
   connectionTimeout="2000"
   redirectPort="8445"/>
   *一般会将tomcat的默认端口号修改为80。80端口号是http协议的默认端口号。
   *好处:在访问时，就不用输入端口号

5．关闭

1. 正常关闭:
   *bin/ shutdown.bat

   ctrl+c

2. 强制关闭:
   *点击言动窗口的x(不推荐使用)

6．配置

部署项目的方式︰
1.直接将项目放到webapps目录下即可。
/ hello:项目的访问路径-->虚拟目录
*简化部署:将项目打成一个war包，再将war包放置到webapps目录下。
war包会自动解压缩
2．配置conf/ server.xml文件
在<Host>标签体中配置
<Context docBase="D: \hello" path=" / hehe"/>

docBase:项目存放的路径
*path :虚拟目录
3．在conf\catalina\localhost创建任意名称的xml文件。在文件中编写
<Context docBase="D: \hello"/>
*虚拟目录:xml文件的名称

动态项目和静态项目:

目录结构︰
java动态项目:
--项目名称
--WEB-INF
-- web.xml :该项目的核心配置文件

-- classes目录:放置字节码文件

-- lib目录∶放置项目依赖的jar包

* 将Tomcat集成到IDEA中，并且创建JavaEE的项目，部署项目。

<img src="C:\Users\ASUS\AppData\Roaming\Typora\typora-user-images\image-20220514103017788.png" alt="image-20220514103017788" style="zoom:50%;" />中添加local的tomcat

添加好了之后 创建javaEE的项目

<img src="C:\Users\ASUS\AppData\Roaming\Typora\typora-user-images\image-20220514103737777.png" alt="image-20220514103737777" style="zoom: 33%;" />选择web applicatioon完成创建

# Servlet:server applet

概念:运行在服务器端的小程序

*Servlet就是一个接口,定义了java类被访问到(tomcat识别)的规则.

*将来我们自定义一个类,实现Servlet接口,复写方法.

## 快速入门:

1. 创建JavaEE项目

2. 定义一个类，实现Servlet接口
	
	public class ServletDemo1 implements Servlet
	
3. 实现接口中的抽象方法

4. 配置Servlet
	 在web.xml中配置：
    <!--配置Servlet -->
    <servlet>
        <servlet-name>demo1</servlet-name>
        <servlet-class>cn.itcast.web.servlet.ServletDemo1</servlet-class>
    </servlet>

    <servlet-mapping>
        <servlet-name>demo1</servlet-name>
        <url-pattern>/demo1</url-pattern>
    </servlet-mapping>

## 执行原理︰

1，当服务器接受到客户端浏览器的请求后，会解析请求URL路径，获取访问的servlet的资源路径

2．查找web.xml文件，是否有对应的<url-pattern>标签体内容。
3，如果有，则在找到对应的<servlet-class>全类名

4.tomcat会将字节码文件加载进内存，并且创建其对象

5．调用其方法

## Serverlet的生命周期及其方法

servlet中的生命周期∶
1．被创建∶执行init方法，只执行一次

- servlet什么时候被创建?
  默认情况下，第一次被访问时，Servlet被创建

  可以配置执行servlet的创建时机。
  *在<servlet>标签下配置
  1．第一次被访问时，创建
  *<load-on-startup>的值为**负数**

  2．在服务器启动时，创建
  <load-on-startup>的值为**0或正整数**

2．提供服务∶执行service方法，执行多次

每次访问servlet时， service方法都会被调用一次。

Servlet的init方法，只执行一次，说明一个servlet在内存中只存在一个对象，Servlet是单例的
*多个用户同时访问时，可能存在线程安全问题。
*解决∶尽量不要在servlet中定义成员变量。即使定义了成员变量，也不要对修改值

3．被销毁∶执行destroy方法，只执行一次
servlet被销毁时执行。服务器关闭时，Servlet被销毁

只有服务器正常关闭时，才会执行destroy方法。
destroy方法在servlet被销毁**之前**执行，一般用于释放资源

> ServeletConfig():获取ServeletConfig对象
>
> ServeletConfig:Servlet配置对象
>
> getServelt:获取Servelet的一些信息,版本,作者等等

## Servlet的注解配置

servlet3.0 :
*好处:
*支持注解配置。可以不需要web.xml 了。
*步骤︰
1．创建JavaEE项目，选择servlet的版本3.0以上，可以不创建web.xml

2．定义一个类，实现servlet接口
3．复写方法
4．在类上使用@webservlet注解，进行配置
@webservlet("资源路径")

# IDEA与tomcat的相关配置

1.IDEA会为每一个tomcat部署的项目单独建立一份配置文件
查看控制台的log : Using CATALINA BASE: “c:\Users\fay\.IntelliJIdea2018.1\system\tomcat、 itcast"
2.工作空间项目(idea上的目录)    和      tomcat部署的web项目(program中的项目)
tomcat真正访问的是"“tomcat部署的web项目”，“tomcat部署的web项目""对应着"工作空间项目”的web目录下的所有资源

WEB- INF目录下的资源不能被浏览器直接访问。
3。断点调试∶使用"小虫子"启动dubug启动

