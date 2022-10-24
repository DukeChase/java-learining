# HTML CSS

## HTML

```html
<!DOCTYPE html>
<html>
    <head>
        <titel></titel>
        <script> type="text/javascript" src="1.js"</script>
        <script type="text/javascript">
        var i=12;
        var j = 13
        alert(i+j)
        </script>
    </head>
    <body>
    <p>hello world</p>
    <div> ...</div>         
    </body>
</html>
```

标签介绍
1. 标签的格式:
	<标签名>封装的数据</标签名>
2. 标签名大小写不敏感。

3. 标签拥有自己的属性。
	i. 分为基本属性：bgcolor="red"             可以修改简单的样式效果
	ii. 事件属性： onclick="alert('你好！');"  可以直接设置事件响应后的代码。
4. 标签又分为，单标签和双标签。
	i. 单标签格式： <标签名 />
		br 换行
		hr 水平线
	ii. 双标签格式: <标签名> ...封装的数据...</标签名>
### 常用标签
超链接
```html
<a href="http://localhost:8080">百度</a><br/>

<a href="http://localhost:8080" target="_self">百度_self</a><br/>

<a href="http://localhost:8080" target="_blank">百度_blank</a><br/>
```

列表标签
```html
<body>

<!--需求 1：使用无序，列表方式，把东北 F4，赵四，刘能，小沈阳，宋小宝，展示出来
ul 是无序列表
type 属性可以修改列表项前面的符号
li 是列表项
-->
	<ul type="none">
		<li>赵四</li>
		<li>刘能</li>
		<li>小沈阳</li>
		<li>宋小宝</li>
	</ul>

</body>
```

表格

跨行跨列表格

表单标签

## CSS层叠样式表
选择器：浏览器根据“选择器”决定受 CSS 样式影响的 HTML 元素（标签）。
属性 (property) 是你要改变的样式名，并且每个属性都有一个值。属性和值被冒号分开，并由花括号包围，这样就组成了一个完整的样式声明（declaration），例如：
`p {color: blue}`

CSS 和 HTML 的结合方式
1. 在标签的style属性上设置 key:value value,修改标签样式。
2. 在 head 标签中，使用 style 标签来定义各种自己需要的 css 样式。
	xxx {key: value value}
3. 把 css 样式写成一个单独的 css 文件，再通过 link 标签引入即可复用。
	`<link rel="stylesheet" type="text/css" href="./styles.css" /> 标`

选择器
1. id选择器  `#id{ key：value;}`
2. class选择器  `.class{key value;}`
3. 组合选择器  `选择器1，选择器2，选择器3{key:value;}`
常用样式
`color:red`
`width:19px`
`height:20px`

## JavaScript
### 基本语法
1. 基本语法：
		1. 与html结合方式
			1. 内部JS：
				- 定义`<script>` 标签体内容就是js代码
			1. 外部JS：
				* 定义`<script>`，通过src属性引入外部的js文件
				* 注意：
				1. `<script>`可以定义在html页面的任何地方。但是定义的位置会影响执行顺序。
				2. `<script>`可以定义多个。
		2. 注释
			1. 单行注释：//注释内容
			2. 多行注释：/*注释内容*/
		3. 数据类型：
			1. 原始数据类型(基本数据类型)：
				1. number：数字。 整数/小数/NaN(not a number 一个不是数字的数字类型)
				2. string：字符串。 字符串  "abc" "a" 'abc'
				3. boolean: true和false
				4. null：一个对象为空的占位符
				5. undefined：未定义。如果一个变量没有给初始化值，则会被默认赋值为undefined
			2. 引用数据类型：对象
		4. 变量
			* 变量：一小块存储数据的内存空间
			* Java语言是强类型语言，而JavaScript是弱类型语言。
				* 强类型：在开辟变量存储空间时，定义了空间将来存储的数据的数据类型。只能存储固定类型的数据
				* 弱类型：在开辟变量存储空间时，不定义空间将来的存储数据类型，可以存放任意类型的数据。
			* 语法：
				* var 变量名 = 初始化值;	
			* typeof运算符：获取变量的类型。
				* 注：null运算后得到的是object
		5. 运算符
			1. 一元运算符：只有一个运算数的运算符
				++，-- ， +(正号)  
				* ++ --: 自增(自减)
					* ++(--) 在前，先自增(自减)，再运算
					* ++(--) 在后，先运算，再自增(自减)
				* +(-)：正负号
			    * 注意：在JS中，如果运算数不是运算符所要求的类型，那么js引擎会自动的将运算数进行类型转换
                    * 其他类型转number：
                        * string转number：按照字面值转换。如果字面值不是数字，则转为NaN（不是数字的数字）
                        * boolean转number：true转为1，false转为0
			2. 算数运算符
				+ - * / % ...
			3. 赋值运算符
				= += -+....
			4. 比较运算符
				> < >= <= == ===(全等于)
				* 比较方式
                  1. 类型相同：直接比较
                      * 字符串：按照字典顺序比较。按位逐一比较，直到得出大小为止。
                  2. 类型不同：先进行类型转换，再比较
                      * ===：全等于。在比较之前，先判断类型，如果类型不一样，则直接返回false
			5. 逻辑运算符
				&&  ||  !
				* 其他类型转boolean：
                   1. number：0或NaN为假，其他为真
                   2. string：除了空字符串("")，其他都是true
                   3. null&undefined:都是false
                   4. 对象：所有对象都为true	
			6. 三元运算符
			 	? : 表达式
				var a = 3;
			    var b = 4;
			    var c = a > b ? 1:0;
				* 语法：
					* 表达式? 值1:值2;
					* 判断表达式的值，如果是true则取值1，如果是false则取值2；
		6. 流程控制语句：
			1. if...else...
			2. switch:
				* 在java中，switch语句可以接受的数据类型： byte int shor char,枚举(1.5) ,String(1.7)
					* switch(变量):
						case 值:
				* 在JS中,switch语句可以接受任意的原始数据类型
			3. while
			4. do...while
			5. for

### 基本对象

1. Function 函数（方法）对象
	1. 创建方式
		1. `var fun = new Function(形式列表参数，方法体)`
		2. `function 方法名称(形式参数列表){方法体}`
		3. `var 方法名 = function(){}`
	2. 方法
	3. 属性
	4. 特点
	5. 调用
2. Array数组对象
3. Boolean
4. Date 日期对象
5. Math 数学对象
6. Number对象
7. String对象
8. RegEXP 正则表达式对象
9. Global对象

### BOM
1. 概念：`Browser Object Model `浏览器对象模型
	* 将浏览器的各个组成部分封装成对象。
2. 组成：
	* Window：	窗口对象
	* Navigator：浏览器对象       not importtan
	* Screen：   显示器屏幕对象   not importtan
	* History：  历史记录对象
	* Location： 地址栏对象
3. `Window`：窗口对象
    1. 创建  
	    * Window对象不需要创建可以直接使用 window.方法名();
	    * window引用可以省略。  方法名();
    2. 方法
         1. 与弹出框有关的方法：
            - `alert()`	显示带有一段消息和一个确认按钮的警告框。
            - `confirm()`	显示带有一段消息以及确认按钮和取消按钮的对话框。
                - 如果用户点击确定按钮，则方法返回true
                - 如果用户点击取消按钮，则方法返回false
            - `prompt()`	显示可提示用户输入的对话框。
                - 返回值：获取用户输入的值
         2. 与打开关闭有关的方法：
            - `close()`	关闭浏览器窗口。
                * 谁调用我 ，我关谁
            - `open()`	打开一个新的浏览器窗口
                * 返回新的Window对象
         3. 与定时器有关的方法
            - `setTimeout()`	在指定的毫秒数后调用函数或计算表达式。
                * 参数：
                    1. js代码或者方法对象
                    2. 毫秒值
                * 返回值：唯一标识，用于取消定时器
            - `clearTimeout()`	取消由 setTimeout() 方法设置的 timeout。
            - `setInterval()`	按照指定的周期（以毫秒计）来调用函数或计算表达式。
            - `clearInterval()`	取消由 setInterval() 设置的 timeout。
    3. 属性：
        1. 获取其他BOM对象：
            `history`
            `location`
            `Navigator`
            `Screen`
        2. 获取DOM对象
            `document`
    4. 特点
        * Window对象不需要创建可以直接使用 window使用。 window.方法名();
        * window引用可以省略。 方法名();
4. `Location`：地址栏对象
	1. 创建(获取)：
		1. `window.location`
		2.`location`
	2. 方法：
		* `reload()`	重新加载当前文档。刷新
	3. 属性
		* `href`	设置或返回完整的 URL。
5. `History`：历史记录对象
    1. 创建(获取)：
        1. `window.history`
        2. `history`
    2. 方法：
        * back()	加载 history 列表中的前一个 URL。
        * forward()	加载 history 列表中的下一个 URL。
        * go(参数)	加载 history 列表中的某个具体页面。
            * 参数：
                * 正数：前进几个历史记录
                * 负数：后退几个历史记录
    3. 属性：
        * length	返回当前窗口历史列表中的 URL 数量。
### DOM
* 概念： Document Object Model 文档对象模型
	* 将标记语言文档的各个组成部分，封装为对象。可以使用这些对象，对标记语言文档进行CRUD的动态操作

* W3C DOM 标准被分为 3 个不同的部分：
	* 核心 DOM - 针对任何结构化文档的标准模型
		* `Document`：  文档对象
		* `Element`：   元素对象
		* `Attribute`： 属性对象
		* `Text`：     文本对象
		* `Comment`:   注释对象
		* `Node`：     节点对象，其他5个的父对象
	* XML DOM - 针对 XML 文档的标准模型
	* HTML DOM - 针对 HTML 文档的标准模型

* 核心DOM模型：
	* `Document`：文档对象
		1. 创建(获取)：在HTML dom 模型中可以使用window对象来获取
			1. window.document
			2. document
		2. 方法：
			1. 获取Element对象：
				1.`getElementById()`	： 根据id属性值获取元素对象。id属性值一般唯一
				2.`getElementsByTagName()`：根据元素名称获取元素对象们。返回值是一个数组
				3.`getElementsByClassName()`:根据Class属性值获取元素对象们。返回值是一个数组
				4.`getElementsByName()`: 根据name属性值获取元素对象们。返回值是一个数组
			2. 创建其他DOM对象：
				 - `createAttribute(name)`
				 - `createComment()`
            	- `createElement()`
            	- `createTextNode()`
		3. 属性
	* `Element`：元素对象
		1. 获取/创建：通过document来获取和创建
		2. 方法：
			1. `removeAttribute()`：删除属性
			2. `setAttribute()`：设置属性
	* `Node`：节点对象，其他5个的父对象
		* 特点：所有dom对象都可以被认为是一个节点
		* 方法：
			* CRUD dom树：
				* `appendChild()`：向节点的子节点列表的结尾添加新的子节点。
				* `removeChild()`：删除（并返回）当前节点的指定子节点。
				* `replaceChild()`：用新节点替换一个子节点。
		* 属性：
			* parentNode 返回节点的父节点。

* HTML DOM
	1. 标签体的设置和获取：`innerHTML`
	2. 使用html元素对象的属性
	3. 控制元素样式
		1. 使用元素的style属性来设置
			如：
				 //修改样式方式1
		        div1.style.border = "1px solid red";
		        div1.style.width = "200px";
		        //font-size--> fontSize
		        div1.style.fontSize = "20px";
		2. 提前定义好类选择器的样式，通过元素的className属性来设置其class属性值。

### 事件监听机制
* 概念：某些组件被执行了某些操作后，触发某些代码的执行。	
	* 事件：某些操作。如： 单击，双击，键盘按下了，鼠标移动了
	* 事件源：组件。如： 按钮 文本输入框...
	* 监听器：代码。
	* 注册监听：将事件，事件源，监听器结合在一起。 当事件源上发生了某个事件，则触发执行某个监听器代码。
	* 常见的事件：
		1. 点击事件：
			1. `onclick`：单击事件
			2. `ondblclick`：双击事件
		2. 焦点事件
			1. `onblur`：失去焦点
			2. `onfocus`:元素获得焦点。
		3. 加载事件：
			1. `onload`：一张页面或一幅图像完成加载。
		4. 鼠标事件：
			1. `onmousedown`	鼠标按钮被按下。
			2. `onmouseup`	鼠标按键被松开。
			3. `onmousemove`	鼠标被移动。
			4. `onmouseover`	鼠标移到某元素之上。
			5. `onmouseout`	鼠标从某元素移开。
		5. 键盘事件：
			1. `onkeydown`	某个键盘按键被按下。	
			2. `onkeyup`		某个键盘按键被松开。
			3. `onkeypress`	某个键盘按键被按下并松开。
	
		6. 选择和改变
			1. `onchange`	域的内容被改变。
			2. `onselect`	文本被选中。
	
		7. 表单事件：
			1. `onsubmit`	确认按钮被点击。
			2. `onreset`	重置按钮被点击。
## Tomcat


## Servlet1
1. 什么是Servlet
	1. Servlet 是 JavaEE 规范之一。规范就是接口
	2. Servlet 就 JavaWeb 三大组件之一。三大组件分别是：**Servlet 程序、Filter 过滤器、Listener监听器**。 
	3. Servlet 是运行在服务器上的一个 java 小程序，它可以接收客户端发送过来的请求，并响应数据给客户端

- Servlet的生命周期
1. 执行Servlet构造器方法
2. 执行init初始化方法
	第一二步，是在第一次访问的时候创建Servlet程序会调用
3. 执行service方法
	第三步，每次访问都会调用
4. 执行destroy销毁方法
	第四步，在web工程停止的时候调用

- 通过继承HttpServlet实现Servlet程序
1. 编写一个类去继承 `HttpServlet` 类
2. 根据业务需要重写 `doGet` 或 `doPost` 方法
3. 到 web.xml 中的配置`Servlet`程序的访问地址

### ServletConfig类

## HTTP协议

 客户端给服务器发送数据叫**请求**。

服务器给客户端回传数据叫**响应**。

请求HTTP协议

GET请求

1. 请求行  GET

2. 请求头
   
   1. key:value

POST请求

1. 请求行  
   1. 请求方式                     POST  
   2. 请求的资源路径[+?+请求参数]  
   3. 请求的协议的版本号            HTTP/1.1
2. 请求头
   1. key:value
3. 空行
4. 请求体

- 响应的HTTP协议
1. 响应行
   1. 响应协议和版本号
   2. 响应状态码
   3. 响应状态描述符
2. 响应头
   1. key:value
3. 空行
4. 响应体

哪些是GET请求，哪些是POST请求
- GET 请求有哪些：
	1、form 标签 `method=get`
	2、a 标签
	3、link 标签引入 css
	4、Script 标签引入 js 文件
	5、img 标签引入图片
	6、iframe 引入 html 页面
	7、在浏览器地址栏中输入地址后敲回车
- POST 请求有哪些：
	8、form 标签 `method=post`

## HttpServletRequest & HttpServletResponse
### HttpServletRequest
a) HttpServletRequest类的作用
每次只要有请求进入 Tomcat 服务器，Tomcat 服务器就会把请求过来的 HTTP 协议信息解析好封装到`Request`对象中。然后传递到service方法（doGet和doPost）中给我们使用。我们可以通过HttpServletRequest对象，获取到所有请求的信息
b) HttpServletRequest类的常用方法
1. `getRequestURI()`      获取请求的资源路径
2. `getRequestURL()`      获取请求的统一资源定位符（绝对路径）
3. `getRemoteHost()`      获取客户端的 ip 地址
4. `getHeader()`         获取请求头
5. `gerParamerter()`      获取请求的参数
6. `getParameterValues()`  获取请求的参数（多个值的时候使用）
7. `getMethod()`          获取请求的方式 GET 或 POST
8. `setAttribute()`       设置域数据
9. `getAttribute()`       获取域数据
10. `getRequestDispacher()`获取请求转发对象
```java
public Serlet1 extends HttpServerlet{
	public void service(){
		
	}
	
	protect void doGet(HttpServletRequest req, HttpServlet resp) throws ServletException, IOException{
	// 处理
	}
}

```

e) 请求的转发
请求转发是指，服务器收到请求后，从一次资源跳转到另一个资源的操作叫请求转发。

### HttpServletResponse
a)HttpServletResponse 类的作用
HttpServletResponse 类和 HttpServletRequest 类一样。每次请求进来，Tomcat 服务器都会创建一个 Response 对象传递给 Servlet 程序去使用。HttpServletRequest 表示请求过来的信息，HttpServletResponse 表示所有响应的信息，我们如果需要设置返回给客户端的信息，都可以通过 HttpServletResponse 对象来进行设置

b)两个输出流的说明。
- getOutputStream() 常用于下载
- getWriter()  常用于回传数据（常用）
两个流同时只能使用一个。
使用了字节流，就不能再使用字符流，反之亦然，否则就会报错。
c) 如何往客户端回传数据
```java
	// 向客户端回传数据
    PrintWriter writer = resp.getWriter();
    writer.wrire("response's content");
```
d) 响应的乱码解决
- 方案一  不推荐
```java
// 设置服务器字符集为 UTF-8
resp.setCharacterEncoding("UTF-8");
// 通过响应头，设置浏览器也使用 UTF-8 字符集
resp.setHeader("Content-Type", "text/html; charset=UTF-8");
```
- 方案二  推荐
```java
// 它会同时设置服务器和客户端都使用 UTF-8 字符集，还设置了响应头
// 此方法一定要在获取流对象之前调用才有效
resp.setContentType("text/html; charset=UTF-8");
```

e) 请求重定向
- 第一种方案(不推荐)：
```java
// 设置响应状态码 302 ，表示重定向，（已搬迁）

resp.setStatus(302);

// 设置响应头，说明 新的地址在哪里

resp.setHeader("Location", "http://localhost:8080");

```

- 第二种方案（推荐使用）：
```java
resp.sendRedirect("http://localhost:8080");
```

## JSP

JSP的三种语法
jsp文件头部声明介绍
`<%@ page language="java" contentType="text/html; charset=UTF-8" pageEncoding="UTF-8" %>`
这是jsp文件的头声明。表示这是jsp页面。
`language` 属性      值只能是 java。 表示翻译的得到的是 java 语言的
`contentType`属性   设置响应头 contentType 的内容
`pageEncoding`属性  设置当前 jsp 页面的编码
`import` 属性       给当前 jsp 页面导入需要使用的类包
`autoFlush` 属性    设置是否自动刷新 out 的缓冲区，默认为 true
`buffer` 属性       设置 out 的缓冲区大小。默认为 8KB
`errorPage` 属性    设置当前 jsp 发生错误后，需要跳转到哪个页面去显示错误信息
`isErrorPage` 属性  设置当前 jsp 页面是否是错误页面。是的话，就可以使用 exception 异常对象
`session` 属性    设置当前 jsp 页面是否获取 session 对象,默认为 true
`extends` 属性    给服务器厂商预留的 jsp 默认翻译的 servlet 继承于什么类

jsp中的三种脚本介绍
1. 声明脚本
	`<%! java code %>`
	在声明脚本块中，我们可以干 4 件事情

	1. 我们可以定义全局变量。
	2. 定义 static 静态代码块
	3. 定义方法
	4. 定义内部类
	几乎可以写在类的内部写的代码，都可以通过声明脚本来实现
2. 表达式脚本(重点，常用)
	`<%= expression here %>`
	表达式脚本 用于向页面输出内容。
	表达式脚本 翻译到 Servlet 程序的 service 方法中 以 out.print() 打印输出
	out 是 jsp 的一个内置对象，用于生成 html 的源代码
	注意：表达式不要以分号结尾，否则会报错
	表达式脚本可以输出任意类型。
	比如：
	1.输出整型
	2.输出浮点型
	3.输出字符串
	4.输出对象
3. 代码脚本(重点，常用)
	`<% java code here %>`
	代码脚本里可以书写任意的 java 语句。
	代码脚本的内容都会被翻译到 service 方法中。
	所以 service 方法中可以写的 java 代码，都可以书写到代码脚本中
jsp中有三种注释：
	1、html注释 
		<!--  html注释  -->
		html注释翻译之后会在_jspService()方法以out.write输出到页面
	2、java注释 
		// 单行注释
		/*  多行注释 */
		java的多行注释在翻译之后在翻译到servlet程序的源代码中
	3、jsp注释 
		<%-- jsp注释 --%>
		jsp注释可以注掉jsp中所有内容，在jsp翻译的时候会被完全忽略掉

jsp九大内置对象
`request`     请求对象，可以获取请求信息
`response`    响应对象。可以设置响应信息
`pageContext` 当前页面上下文对象。可以在当前上下文保存属性信息
`session`  会话对象。可以获取会话信息。
`exception` 异常对象只有在 jsp 页面的 page 指令中设置 isErrorPage="true" 的时候才会存在
`application`  ServletContext 对象实例，可以获取整个工程的一些信息。
`config`   ServletConfig 对象实例，可以获取 Servlet 的配置信息
`out`  输出流
`page`  表示当前 Servlet 对象实例（无用，用它不如使用 this 对象）。
九大内置对象，都是我们可以在【代码脚本】中或【表达式脚本】中直接使用的对象。
JSP标签
jsp 静态包含
```jsp
<%--
<%@ include file=""%> 就是静态包含
file 属性指定你要包含的 jsp 页面的路径
地址中第一个斜杠 / 表示为 http://ip:port/工程路径/ 映射到代码的 web 目录
静态包含的特点：
1、静态包含不会翻译被包含的 jsp 页面。
2、静态包含其实是把被包含的 jsp 页面的代码拷贝到包含的位置执行输出
--%>

<%@ include file="/include/footer.jsp"%>

```
jsp动态包含
```jsp
<%--
<jsp:include page=""></jsp:include>
这是动态包含
page 属性是指定你要包含的 jsp 页面的路径
动态包含也可以像静态包含一样。把被包含的内容执行输出到包含位置
动态包含的特点：
1、动态包含会把包含的 jsp 页面也翻译成为 java 代码
2、动态包含底层代码使用如下代码去调用被包含的 jsp 页面执行输出。
JspRuntimeLibrary.include(request, response, "/include/footer.jsp", out, false);
3、动态包含，还可以传递参数
--%>

<jsp:include page="/include/footer.jsp">

<jsp:param name="username" value="bbj"/>

<jsp:param name="password" value="root"/>

</jsp:include>
```
jsp标签-转发

```jsp
<%--

<jsp:forward page=""></jsp:forward> 是请求转发标签，它的功能就是请求转发

page 属性设置请求转发的路径

--%>
<jsp:forward page="/scope2.jsp"></jsp:forward>
```
## Cookie Session


## JQuery
概念
$是JQuery的核心函数，能完成JQuery的很多功能。` $()`就是调用`$`这个函数
1. 传入参数为函数时
	表示页面加载完成之后。相当于window.onload = function(){}
2. 传入参数为 HTML 字符串时
	会对我们创建这个HTML标签对象
3. 传入参数为 选择器字符串时：
	`$(“#id 属性值”);`    id 选择器，根据 id 查询标签对象
    `$(“标签名”); `      标签名选择器，根据指定的标签名查询标签对象
    `$(“.class 属性值”);` 类型选择器，可以根据 class 属性查询标签对象
4. 传入参数为DOM对象时：
	会把这个 dom 对象转换为 jQuery 对象

jQuery对象和dom对象区分

选择器
基本选择器
层级选择器

## JSON AJAX
### JSON
```javascript
var jsonObj = {
"key1":12,
"key2":"abc",
"key3":true,
"key4":[11,"arr",false],
"key5":{"key5_1" : 551,
"key5_2" : "key5_2_value"
},
"key6":[{"key6_1_1":6611,"key6_1_2":"key6_1_2_value"},
{"key6_2_1":6621,"key6_2_2":"key6_2_2_value"}]

};
```
### AJAX
jQuery 中的AJAX
`$.ajax`

`$.get  $.post`

`$.getJSON`

## Redis

数据类型
字符串String
散列表hash map
列表List
集合Set
有序集合

