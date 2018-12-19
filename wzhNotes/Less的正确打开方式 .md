@[Less笔记](这里写自定义目录标题)

# 前言

## CSS短板

&emsp;&emsp;作为前端学习者的我们，或多或少都要学习一些CSS，它作为前端开发三大基石之一，时刻引领着Web的发展方向。而CSS作为一门标语言，可能给初学者的印象是简单易懂，毫无逻辑，而且选择器及样式重复率高，不像编程该有的样子。在语法更新时，每当CSS新属性的提出，又会成为浏览器的兼容性问题的绊脚石。一言以蔽之，CSS的短板不容忽视。
<br>
&emsp;&emsp;问题的诞生往往伴随着新技术的兴起，在Web飞速发展的这几年，为了让CSS富有逻辑性，更有效率，涌现出了一些神奇的预处理语言。它们让CSS彻底变成一门可以使用变量、循环、继承、自定义方法等多种特性的标记语言，逻辑性得到大大的增强。

## 预处理语言的诞生

* **Sass**
<br>
Sass诞生于2007年，Ruby编写，其功能及语法都十分全面，可以说完全把CSS变成了一门编程语言，在国内外都十分受欢迎。是一门非常优秀的的预处理语言。
* **Stylus**
<br>
Stytus诞生于2010年，来自Node.js社区，其语法功能与Sass不相伯仲，是一门十分独特的创新型语言。
* **Less**
<br>
Less诞生于2009年，受Sass影响创建的一个开源项目。它扩充了CSS语言，增加了诸如变量、混合、函数等功能，让CSS更易于维护、方便。

## 预处理语言的选择

&emsp;&emsp;这是一个十分纠结的问题。
<br>
&emsp;&emsp;在网上讨论看来，Sass 与 Stylus 相比于 Less 功能更为丰富，但对于学习成本以及适应时间 ，Less 稍胜一筹。Less 没有去掉任何 CSS 的功能，而是在现有的语法上，增添了许多额外的功能特性，所以学习 Less 是一件非常舒服的事情。
<br>
&emsp;&emsp;如果你之前没有接触过预处理语言，纠结应该学哪一个，不如先看看 下面 Less 的介绍，我相信你会爱上它的。

## Less的正确打开方式 

1. 在页面中引用Less.js
<br>
可以在[官网](https://www.css88.com/doc/less/#)下载或者使用[CDN](//cdnjs.cloudflare.com/ajax/libs/less.js/2.7.2/less.min.js)
```js
<script src="//cdnjs.cloudflare.com/ajax/libs/less.js/2.7.2/less.min.js"></script>
```
&emsp;&emsp;&emsp;
需要注意的是，link标签一定要在引入Less.js之前引入，并且link标签的的rel属性要设置为stylesheet/less
```js
<link rel="stylesheet/less" herf="style.less">
<script src="//cdnjs.cloudflare.com/ajax/libs/less.js/2.7.2/less.min.js"></script>
```
2. 在命令行，使用Node包管理工具npm来安装:
```
npm install -g less 
```
&emsp;&emsp;&emsp;一旦安装完成，就可以在命令行中调用，例如:
```
lessc styles.less
```
&emsp;&emsp;&emsp;这样的话编译后的CSS将会输出到 'stdout' 中，你可以选择将这个输出重定向到文件中:
```
$ lessc styles.less > styles.css
```
&emsp;&emsp;&emsp;详细步骤请参考官方文档
* 如果你在本地环境，可以使用第一种方式，非常简单；但在生产环境中，性能非常重要，最好使用第二种方式

# 正文
* Less的功能特性
## 变量（Variables）
&emsp;&emsp;我们常常在CSS中看到同一个值重复出现了了很多次，这样不仅降低效率，还使得代码难以维护。
<br>
&emsp;&emsp;**变量**通过为你提供一种在一个地方管理这些值的方法让你的代码变得更容易维护（值得一提的是，其变量是常量 ，所以只能定义一次，不能重复使用。
值变量）
### 值变量
以@开头定义变量，并且使用时直接键入@名称
```less
/* less */
//定义值变量
@color: #999; 
@bgColor: skyblue; //不要添加引号
@width: 50%;
//使用值变量
#warp { 
  color: @color;
  width: @width;
}

/* 生成后的CSS */
 #wrap {
  color: #999;
  width: 50%;
}
```
在平时工作中，我们可以把变量封装到一个文件中，这样有利于代码的组织维护。
```less
@lightPrimaryColor: #c5cae9;
@textPrimaryColor: #fff;
@accentColor: rgb(99,137,185;
@primaryTextColor: #646464;
@secondaryTextColor: #000;
@dividerColor: #b6b6b6;
@borderColor: #dadada;
```
### 选择器及属性变量 
让选择器或者属性名变成动态值
```less
/* Less */
//定义选择器变量
@mySelector: #wrap;
@Wrap: wrap;
@{mySelector}{ //变量名 必须使用大括号包裹
  color: #999;
  width: 50%;
}
.@{Wrap}{
  color:#ccc;
}
#@{Wrap}{  
  color:#666;
}

/* 生成的 CSS */
#wrap{ 
  color: #999;
  width: 50%;
}
.wrap{
  color:#ccc;
}
#wrap{  
  color:#666;
}
```
### url变量
项目结构修改时，改变其变量名就好
```less
/* Less */
@images: "../img";//需要加引号
body {
  background: url("@{images}/dog.png");//变量名 必须使用大括号包裹
}

/* 生成的 CSS */
body {
  background: url("../img/dog.png");
}
    
```
### 声明变量
类似于混合方法
```less
-结构：@name: { 属性：值 }
-使用：@name()
```
```less
 /* Less */
@background: {background:red;};
#main{
  @background();
}
@Rules:{
  width: 200px;
  height: 200px;
  border: solid 1px red;
};
#con{
  @Rules();
}

/* 生成的 CSS */
#main{
  background:red;
}
#con{
  width: 200px; 
  height: 200px;
  border: solid 1px red;
}
```
### 变量运算
任何数值，颜色和变量都可以进行运算，=-*/都可以，计算一方带单位就好
```less
/* Less */
@width:300px;
@color:#222;
#wrap{
  width:@width-20;
  height:@width-20*5;
  margin:(@width-20)*5;
  color:@color*2;
  background-color:@color + #111;
}

/* 生成的 CSS */
#wrap{
  width:280px;
  height:200px;
  margin:1400px;
  color:#444;
  background-color:#333;
}   
```
### 变量的作用域
延迟加载，块级作用域
<br>Less 中的作用域与编程语言中的作用域概念非常相似。首先会在局部查找变量和混合，如果没找到，编译器就会在父作用域中查找，依次类推。
```less
/* Less */
@var: @a;
@a: 100%;
#wrap {
  width: @var;
  @a: 9%;
}

/* 生成的 CSS */
#wrap {
  width: 9%;
}
```
## 嵌套（Nested）
模仿了 HTML 的结构，代码更简洁
```less
/* Less */
#header {
  color: black;
  .navigation {
    font-size: 12px;
  }
  .logo {
    width: 300px;
  }
}

/* 生成的 CSS */
#header {
  color: black;
}
#header .navigation {
  font-size: 12px;
}
#header .logo {
  width: 300px;
}
```
### **&** 的妙用
& ：代表的上一层选择器的名字，此例便是header
* 要点：
<br>
  `.` 与 `#` 皆可作为 方法前缀。
<br>
  方法后写不写 `()` 看个人习惯。
```less
/* Less */
#header{
  &:after{
    content:"Less is more!";
  }
  .title{
    font-weight:bold;
  }
  &_content{//理解方式：直接把 & 替换成 #header
    margin:20px;
  }
}
/* 生成的 CSS */
#header:after{
  content:"Less is more!";
}
#header .title{ //嵌套了
  font-weight:bold;
}
#header_content{//没有嵌套！
    margin:20px;
}
```
## 混合（Mixins）
混合就是一种将一系列属性从一个规则集引入(“混合”)到另一个规则集的方式。
### 普通混合（无参数）
方法犹如 声明的集合，使用时 直接键入名称即可
```less
/* Less */
.card { // 等价于 .card()
    background: #f6f6f6;
    -webkit-box-shadow: 0 1px 2px rgba(151, 151, 151, .58);
    box-shadow: 0 1px 2px rgba(151, 151, 151, .58);
}
#wrap{
  .card;//等价于.card();
}
/* 生成的 CSS */
#wrap{
  background: #f6f6f6;
  -webkit-box-shadow: 0 1px 2px rgba(151, 151, 151, .58);
  box-shadow: 0 1px 2px rgba(151, 151, 151, .58);
}
```
### 传参混合
Less 可以使用默认参数，如果 没有传参数，那么将使用默认参数。
<br>
@arguments 犹如 JS 中的 arguments 指代的是 全部参数。
<br>
传的参数中 必须带着单位。


