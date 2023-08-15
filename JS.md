# js注释

```javascript
// 单行注释
/* 多行注释*/
```

## JS运算符

[JS运算符](https://www.w3school.com.cn/js/js_operators.asp)

# [JavaScript数据类型](https://www.w3school.com.cn/js/js_datatypes.asp)

字符串，数值，布尔值，数组，对象

* JavaScript 拥有动态类型

* JavaScript 从左向右计算表达式。不同的次序会产生不同的结果：

```javascript
var x = 911 + 7 +'Porsche'   // 918Prosche
```

* js数组

```javascript
var cars = ["Porsche", "Volvo", "BMW"]
```

* js对象

```javascript
var person = {firstName:"Bill", lastName:"Gates", age:62, eyeColor:"blue"};
```

* typeof  运算符
* Undefined
* 空值
* null
* 对象

# JS函数

```javascript
function functionName (arg1, arg2){
   // code
    return 0;
}
```



## 函数调用

* 当事件发生时
* 当JavasScript代码调用时
* 自动的（自调用）

访问没有 () 的函数将返回函数定义

# JS对象
```javascript
var car = {type = "porsche", model = "911", color:"red"};

var person = {
  firstName: "Bill",
  lastName : "Gates",
  id       : 678,
  fullName : function() {
    return this.firstName + " " + this.lastName;
  }
};
```
## JS事件

```javascript
<element event = 'some JavaScript code'>
```

* 常见的HTML事件

| 事件        | 描述               |
| ----------- | ------------------ |
| onchange    | HTML元素被改变     |
| onclick     | 用户点击了HTML元素 |
| onmouseover |                    |
| onmouseout  |                    |
| onkeydown   |                    |
| onload      |                    |

# [字符串](https://www.w3school.com.cn/js/js_string_methods.asp)

* 字符串长度 length

```javascript
var txt = "ABCDEFGHIJKLMNOPQRSTUVWXYZ";
vat sln = txt.length
```

* 查找字符串中的字符串  

indexOF()    lastIndexOf()

* 检索字符串中的字符串

search()

* slice()
* substring()
* substr()
* replace()
* toUpperCase()
* toLowerCase()
* concat()
* trim()
* charAt()   charCodeAt()
* split()

# JS数字

JavaScript数值始终是64位的浮点数

## JS数字方法

* toString()
* toExponential()
* toFixed()
* toPrecision()
* valueOf()

# JS数组

## 数组方法

## 数组排序

## 数组迭代



# JS日期

# vue

每个 Vue 应用都需要通过实例化 Vue 来实现。

```javascript
 var vm = new Vue({
        el: '#vue_det',  // 
        data: {
            site: "菜鸟教程",
            url: "www.runoob.com",
            alexa: "10000"
        },
        methods: {
            details: function() {
                return  this.site + " - 学的不仅是技术，更是梦想！";
            }
        }
     	filters:{   // 过滤器
 		}
        computed:{
              site:{
                  // getter
                  get:function(){
     					return  this.xxx
 					}
				  // setter
				  set:function(){                      
                  	}
                  }    
 		}
    })
```



# 缩写 

```html
<!-- 完整语法 -->
<a v-bind:href="url"></a>
<!-- 缩写 -->
<a :href="url"></a>

<!-- 完整语法 -->
<a v-on:click="doSomething"></a>
<!-- 缩写 -->
<a @click="doSomething"></a>
```

## 指令

指令是带有 v- 前缀的特殊属性。

* 使用 v-html 指令用于输出 html 代码

* v-if

* v-else

* v-else-if

* v-show

* v-for

循环使用 v-for 指令。

v-for 指令需要以 **site in sites** 形式的特殊语法， sites 是源数据数组并且 site 是数组元素迭代的别名。

