

[TOC]

## 概念

概念：	一门客户端脚本语言

​	* 运行在客户端浏览器中的。每一个浏览器都有JavaScript的解析引擎

​	* 脚本语言：不需要编译，直接就可以被浏览器解析执行了

 功能：

​	* 可以来增强用户和html页面的交互过程，可以来控制html元素，让页面有一些动态的效果，增强用户的体验。

JavaScript = ECMAScript + JavaScript自己特有的东西(BOM+DOM)

ECMAScript：客户端脚本语言的标准

BOM:Browser Object Model 浏览器对象模型

DOM:

## ECMAScript

### 基础语法

1. 与HTML的结合方式

   1. 内部JS

      定义<script>，标签体内容就是js代码

   2. 外部JS

      定义<script>，通过src属性引入外部的js文件

   3. 注意:

      1. <script>可以定义在html页面的任何地方。但是定义的位置会影响执行顺序。

      2. <script>可以定义多个
          1.<script>alert("hello")</script>
          2.<script src="js/a.js"> </script>

2. 注释

   1. 单行注释：//注释内容
   2. 多行注释：/\*注释内容*/

3. 数据类型

   1. 原始数据类型(基本数据类型)

      1. number：数字。 整数/小数/NaN(not a number 一个不是数字的数字类型)
      2. string：字符串。 字符串  "abc" "a" 'abc'
      3.  boolean: true和false
      4.  null：一个对象为空的占位符
      5.  undefined：未定义。如果一个变量没有给初始化值，则会被默认赋值为undefined

   2. 引用数据类型

      对象

4. 变量

   1. 变量：一小块存储数据的内存空间

      Java语言是强类型语言，而JavaScript是弱类型语言。

      强类型：在开辟变量存储空间时，定义了空间将来存储的数据的数据类型。只能存储固定类型的数据

      弱类型：在开辟变量存储空间时，不定义空间将来的存储数据类型，可以存放任意类型的数据。

   2. 语法

      * var 变量名 = 初始化值;

      * typeof运算符：获取变量的类型。

         注：null运算后得到的是object

5. 运算符

  
  
  1. 一元运算符
  
     只有一个运算数的运算符
  
     ++ , --  ,  +(正号)
  
      * ++ (--): 自增(自减)
  
      * ++(--) :在前，先自增(自减)，再运算
  
      * ++(--) :在后，先运算，再自增(自减)
  
      * +(-): 正负号
  
      * 注意：在JS中，如果运算数不是运算符所要求的类型，那么js引擎会自动的将运算数进行类型转换
  
        其他类型转number：
  
           * string转number：按照字面值转换。如果字面值不是数字，则转为NaN（不是数字的数字）
           * boolean转number：true转为1，false转为0
  
        
  
  2. 算数运算符
  
     +,-,*,/,%
  
  3. 赋值运算符
  
     =, += , -= , /= ,*= , %=
  
  4. 比较运算符
  
     \>    <   \>=  <=   ==  ===(全等于) 
  
     * 比较方式
              1. 类型相同：直接比较
                 * 字符串：按照字典顺序比较。按位逐一比较，直到得出大小为止。
              2. 类型不同：先进行类型转换，再比较
                 * ===：全等于。在比较之前，先判断类型，如果类型不一样，则直接返回false 
  
  5. 逻辑运算符
  
     &&   ||   !
  
     * 其他类型转boolean：
              1. number：0或NaN为假，其他为真
              2. string：除了空字符串("")，其他都是true
              3. null&undefined:都是false
              4. 对象：所有对象都为true
  
  6. 三元运算符
  
     ?  :   表达式
  
5. 流程控制语句

  1. if...else...
  1. switch:
  				* 在java中，switch语句可以接受的数据类型： byte int shor char,枚举(1.5) ,String(1.7)
  					* sswitch(变量):
  						case 值:
  	
  	   * 在JS中,switch语句可以接受任意的原始数据类型
  3. while
  4. do...while
  5. for
  
5. JS特殊语法

  1. 语句以;结尾，如果一行只有一条语句则 ;可以省略 (不建议)	
  1.  变量的定义使用var关键字，也可以不使用
  	   * 用： 定义的变量是局部变量
       * 不用：定义的变量是全局变量(不建议)

### 基本对象

#### 1.Function:函数(方法)对象

1. 创建

     1. var fun = new Function(形式参数列表,方法体);  //忘掉

       ```html
       <script>
       var fun =new Function("a","b","alert(a)");
           fun(1,2);
       </script>
       ```

       

     1. function 方法名称(形式参数列表){
           方法体
         }

   3. var 方法名 = function(形式参数列表){
           方法体
      }

   方法：

2. 属性：
   length:代表形参的个数

3. 特点：

   1. 方法定义时，形参的类型不用写,返回值类型也不写。
   2. 方法是一个对象，如果定义名称相同的方法，会覆盖
   3. 在JS中，方法的调用只与方法的名称有关，和参数列表无关
   4. 在方法声明中有一个隐藏的内置对象（数组），arguments,封装所有的实际参数

4. 调用：
   方法名称(实际参数列表);

#### 2.Array:数组对象

  1. 创建：
                   1. var arr = new Array(元素列表);
                   2. var arr = new Array(默认长度);
                   3. var arr = [元素列表];
    2. 方法
          join(参数):将数组中的元素按照指定的分隔符拼接为字符串
          push()	:向数组的末尾添加一个或更多元素，并返回新的长度。
  3. 属性
        length:数组的长度
  4. 特点：
        1. JS中，数组元素的类型可变的。
        2. JS中，数组长度可变的。

#### 3.Boolean对象

#### 4.Date:日期对象

            1. 创建：
                var date = new Date();
    
        2. 方法：
            `toLocaleString()`：返回当前date对象对应的时间本地字符串格式
            `getTime()`:获取毫秒值。返回当前如期对象描述的时间到1970年1月1日零点的毫秒值差

#### 5.Math: 数学对象

  1. 创建：
       特点：Math对象不用创建，直接使用。  Math.方法名();
       
  2. 方法：
        random():返回 0 ~ 1 之间的随机数(小数,整数)。 含0不含1 [0,1)
        ceil(x)：对数进行上舍入。
        floor(x)：对数进行下舍入。
        round(x)：把数四舍五入为最接近的整数。

  3. 属性：
          PI

习题:输出从1~100的随机**整数**

#### 6.RegExp:正则表达式

1．正则表达式:定义字符串的组成规则。

1. 单个字符:[]
   如: [a] [ab] [a-zA-Z0-9\_]
   *特殊符号代表特殊含义的单个字符:
   \d:单个数字字符[o-9]
   \w:单个单词字符[a-zA-Z0-9_]

2. 量词符号∶
   ?:表示出现0次或1次

   *∶表示出现0次或多次

   +∶出现1次或多次
   {m, n}:表示m<=数量<= n
   *m如果缺省: {,n}:最多n次

   n如果缺省:{m,}最少m次

2．正则对象:

1. 创建

   var reg = new RegExp("正则表达式");

   2. var reg =/正则表达式/;

2. 方法

1. test(参数):验证指定的字符串是否符合正则定义的规范

   返回boolean值

```js
    var a="abcdgjdsankj";
    var reg1=new RegExp("^\\w{6,12}$");
// 字符串中 一个\表示转义字符 要想表示\w的含义,要加两个\\
    var reg2=/^\w{6,12}$/;
//注意第二种方法不要加" "字符串	
    alert(reg1.test(a));
```

#### 7.Global对象

1. 特点:全局对象，这个Global中封装的方法不需要对象就可以直接调用。
   方法名();

2. 方法:
   `encodeURI( )` : url编码
   `decodeURI( )` : url解码
   `encodeURIComponent( )` : url编码,编码的字符更多`decodeURIComponent( ) `: url解码
   `parseInt()`:将字符串转为数字

   `isNAN()`:

   *逐—判断每一个字符是否是数字，直到不是数字为止，将前边数字部分转为numberisNaN():判断一个值是否是NaN
   *NaN六亲不认，连自己都不认。NaN参与的==比较全部为false
   `eval()`:讲JavaScript字符串，并把它作为脚本代码来执行。

3. .URL编码
   传智播客=%E4%BC%A0%E6%99%BA%E6%92%AD%E5%AE%A2

# Dom的简单学习

DOM简单学习:为了满足案例要求

*功能:控制html文档的内容
*代码︰获取页面标签(元素)对象Element
*document.getElementById("id值"):通过元素的id获取元素对象

alert(获取的对象名): 弹出对象是否获取成功的样式.

*操作Element对象:

1.修改属性值:

1. 明确获取的对象是哪一个?
2. 查看API文档，找其中有哪些属性可以设置

2.修改标签体内容∶
属性: innerHTML

```js
<img id="ligth" src="img/off.gif" >
<div id="word"> 哈哈哈哈哈哈 </div>
<script>
    var ligth=document.getElementById("ligth");
    // alert(ligth);
    //搞一个动态变化
    alert("我要换图片了");
    ligth.src="img/on.gif";
     alert(ligth);
     var word=document.getElementById("word");
    alert("我要换内容了");
    alert(word);
    word.innerHTML="呵呵呵呵呵呵";

</script>
```

# 事件的简单学习

*功能∶某些组件被执行了某些操作后，触发某些代码的执行。
*造句:xxx被xxx,我就xxx
*我方水晶被摧毁后，我就责备对友。

*敌法方水晶被摧毁后，我就夸奖自己。
*如何绑定事件
1.直接在html标签上，指定事件的属性(操作)，属性值就是js代码
          1．事件: onclick---单击事件
2．通过js获取元素对象，指定事件属性，设置一个函数
*属性: innerHTML

# Bom

1.概念∶Browser object Model 浏览器对象模型
*将浏览器的各个组成部分封装成对象。
2．组成︰

- window :窗口对象
- *Navigator :浏览器对象
- *screen :显示器屏幕对象
- History :历史记录对象
- Location :地址栏对象

## window:窗口对象

1．创建
2．方法
1．与弹出框有关的方法:
`alert()`显示带有一段消息和一个确认按钮的警告框。
`confirm()`显示带有一段消息以及确认按钮和取消按钮的对话框。
*如果用户点击确定按钮，则方法返回true
*如果用户点击取消按钮，则方法返回false

`prompt()`显示可提示用户输入的对话框。
*返回值:获取用户输八的值

2.与开发关闭有关的方法:
close()关闭浏览器窗口。
  *谁调用我，我关谁
open()打开一个新的浏览器窗口
 *返回新的window对象
3.与定时器有关的方式
`setTimeout()`:在指定的毫秒数后调用函数或计算表达式。
*参数:

1. js代码或者方法对象
2. 毫秒值
  *返回值:唯一标识，用于取消定时器

`clearTimeout()`取消由setTimeout()方法设置的 timeout。
`setInterval()`
按照指定的周期（以毫秒计）来调用函数或计算表达式。
`clearInterval()` 取消由setInterval()设置的 timeout。

3．属性
1．获取其他BOM对象:
history
location

Navigator

screen 

2.获取DOM对象
document

4．特点
*window对象不需要创建可以直接使用window使用。*

*window.方法名();*window引用可以省略。方法名();

## location :地址栏对象

记住是小写的location!!!

1.创建(获取)∶

1. window. location
2.  location

2.方法︰
reload() 重新加载当前文档。刷新

3．属性
*href   设置或返回完整的URL

## History:历史记录对象

1．创建(获取):

1. window.history
2.  history

2．方法:
`back( )`加载history列表中的前一个 URL

`forward()`加载history列表中的下一个URL。

`go(参数)`加载history列表中的某个具体页面。
参数:
正数:前进几个历史记录

负数:后退几个历史记录
3．属性:
来length返回当前窗口历史列表中的 URL数量。

# Dom

概念: Document Object Model文档对象模型
*将标记语言文档的各个组成部分，封装为对象。可以使用这些对象
对标记语言文档进行CRUD的动态操作
W3C DOM 标准被分为3个不同的部分∶

1. 核心DOM  - 针对任何结构化文档的标准模型

   `Document` :文档对象
   `Element` :元素对象

   `Attribute` :属性对象

   `Text` :文本对象
   `Comment`:注释对象

   

   `Node`:节点对象，其他5个的父对象

2. XML DOM -针对XML文档的标准模型

3. HTML  DOM -针对HTML文档的标准模型

## 核心DOM模型

### Document :文档对象

1．创建(获取):在html dom模型中可以使用window对象来获取

1. window.document
2. document

2．方法:
        1.获取Element对象:

1. `getElementById()` :根据id属性值获取元素对象。id属性值一般唯一
2. `getElementsByTagName()`:根据元素名称获取元素对象们。返回值是一个数组
3. `getElementsByClassName()`:根据class属性值获取元素对象们。返回值是一个数组
4.  `getElementsByName()`:根据name属性值获取元素对象们。返回值是一个数组

​       2.创建其他Dom对象

1. createAttribute( name)
2. createComment()
3. createElement()
4. createTextNode()

也可以给新创建的对象 设置样式<style>
不过要给新的对象 设置属性值

3.属性

length

## Element :元素对象

1．获取/创建

 通过document来获取和创建

2．方法∶

1. removeAttribute( ) :删除属性
1.  setAttribute( ) :设置属性

Node :节点对象。其他5个的父对象

特点∶所有dom对象都可以被认为是一个节点

方法∶
CRUD dom树∶
`appendchild()`:向节点的子节点列表的结尾添加新的子节点。

`removechild() `:删除(并返回)当前节点的指定子节点。

`replacechild()`:用新节点替换一个子节点。

使用方法          父节点.方法(要进行操作的子节点)

属性

`parentNode`:返回节点的父节点

超链接功能:(用a标签实现按钮功能)
1.可以被点击:样式
2.点击后跳转到href指定的url
需求:保留1功能，去掉2功能
实现: href="javascript:void(0)"

## HTML  DOM

1. 标签体的设置和获取 : innerHTML

   1. 替换

      获取的document对象.innerHTML=" js语句".

   2. 追加

      获取的document对象.innerHTML +=" js语句".

2. 使用html元素对象的属性

   用到的时候去表查看

3. 控制样式

   - 使用元素的style属性来设置
     如:
     /修改样式方式1
     div1.style.border = "1px solid red";

     div1.style.width = "200px" ;
     //font-size--> fontsize
     div1.style.fontSize = "20px" ;

   - 提前定义好类选择器的样式，通过元素的className属性来设置器class属性值。

## Dom Event 事件

事件监听机制∶

- 概念:某些组件被执行了某些操作后，触发某些代码的执行。
- 事件:某些操作。如:单击，双击，键盘按下了，鼠标移动了

事件:某些操作.

事件源:组件。如:按钮文本输入框...

监听器:代码。

注册监听∶将事件，事件源，监听器结合在一起。当事件源上发生了某个事件，则触发执行某个监听器代码。

常见的事件

1. 点击事件∶

   1. `onclick`:单击事件
   2. `ondblclick` :双击事件

2. 焦点事件

   1. `onblur` :失去焦点

      一般用于表单验证

   2.  `onfocus`:元素获得焦点。

3. 加载事件∶

   `onload` : 一张页面或一幅图像完成加载。

4. 鼠标事件︰

   1. `onmousedown `  鼠标按钮被按下。

      定义方法时,可以定义一个形参,接受`event`对象

      event对象的`button`属性可以获取鼠标按钮键被点击了

   2. `onmouseup `  鼠标按键被松开

   3. `onmousemove` 鼠标被移动。

   4. `onmouseover`鼠标移到某元素之上。

   5.  `onmouseout`鼠标从某元素移开。

5. 键盘事件:

   1. `onkeydown`某个键盘按键被按下。
   
      event对象的`keyCode`属性可以获取键盘按钮键被点击了

      输入字母时获得的keyCode总是229。是因为是中文输入法

      输入法截流了
   
   2. `onkeyup`某个键盘按键被松开。
   
   3. `onkeypress`某个键盘按键被按下并松开。
   
   6．选择和改变
   
   1. `onchange`  域的内容被改变。
   2. `onselect`  域中的文本被选中。
   
   7．表单事件:
   
   1. `onsubmit ` 确认按钮被点击。
   2. ` onreset`   重置按钮被点击。
