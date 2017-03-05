# CSS 指层叠样式表 (Cascading Style Sheets)

## 优先级和多重
1. 浏览器缺省设置
2. 外部样式表
    ```HTML
    <head>
    <link rel="stylesheet" type="text/css" href="mystyle.css" />
    </head>
    ```
    ```CSS
    p {background-color: red;}
    ```
3. 内部样式表（位于\<head>标签内部）
    ```HTML
    <head>
    <style type="text/css">
      hr {color: sienna;}
      p {margin-left: 20px;}
      body {background-image: url("images/back40.gif");}
    </style>
    </head>
    ```
4. 内联样式（在 HTML 元素内部）
    ```HTML
    <p style="color: sienna; margin-left: 15px;">
    This is a paragraph
    </p>
    ```

多重样式合并后：
```CSS
p {
    background-color: red;
    color: sienna;
    margin-left: 15px;
}
```

## 语法
CSS 规则由两个主要的部分构成：选择器，以及一条或多条声明  
```CSS
selector {
    declaration1;
    declaration2;
    ...
    declarationN
    }
```
e.g.  
```CSS
h1 {
    color: red;
    font-size: 14px;
    }
```
![](http://www.w3school.com.cn/i/ct_css_selector.gif)

一个完整的CSS语句：
```CSS
body {
  color: #000;
  background: #fff;
  margin: 0;
  padding: 0;
  font-family: Georgia, Palatino, "sans serif";
  }
```

## 继承
```HTML
<body>
    <p>Shopping List</p>
    <ol>
        <li>xxxx</li>
        <li>xxxx</li>
        <li>xxxx</li>
    </ol>
    <input type="button" value="Submit" onclick="alert('Happy shopping!')">
</body>
```

```CSS
body {
     font-family: Verdana, sans-serif;
     }

td, ul, ol, ul, li, dl, dt, dd {
     font-family: Verdana, sans-serif;
     }

p {
     font-family: Times, "Times New Roman", serif;
     }
```

## 选择器
### 元素选择器

#### 选择器分组
```CSS
/* no grouping */
h1 {color:blue;}
h2 {color:blue;}
h3 {color:blue;}
h4 {color:blue;}
h5 {color:blue;}
h6 {color:blue;}

/* grouping */
h1, h2, h3, h4, h5, h6 {color:blue;}
```

#### 声明分组
```CSS
/* no grouping */
h1 {font: 28px Verdana;}
h1 {color: blue;}
h1 {background: red;}

/* grouping */
h1 {
    font: 28px Verdana;
    color: white;
    background: black;
    }
```

### 类选择器 .
```HTML
<h1 class="first">
My First Heading
</h1>

<p class="first html">
My first html paragraph.
</p>
```

```CSS
*.first {color:red;}
.first {color:red;}
p.first {color:red;}
p.html {color:red;}
.first.html {color:red;}
h1.first {color:blue;}
```

### ID选择器 #
```HTML
<ul id="drink" type="square">
    <li>Coffee</li>
    <li>Tea</li>
    <li>Milk</li>
</ul>
```
```CSS
*#drink {font-weight:bold;}
#drink {font-weight:bold;}
ul#drink {font-weight:bold;}
```

**注意！**
1. ID只能使用一次
2. 一个元素不能有多个ID
3. 区分大小写

### 属性选择器
```HTML
<img src="http://www.huawei.com/Assets/CBG/img/logo.png" alt="The logo of Huawei"><br/>
<a href="http://www.huawei.com" target="_blank">Open Huawei official website in a new window.</a><br/>
Click the logo --><a href="http://www.huawei.com"><img src="http://www.huawei.com/Assets/CBG/img/logo.png"
                                                       align="middle"/></a><br/>
```
```CSS
*[src] {color:red;}
a[href] {color:red;}
img[src][alt] {border: 5px solid red;}
a[target="_blank"] {color: red;}
img[src="http://www.huawei.com/Assets/CBG/img/logo.png"][align="middle"] {color: red;}
```
**提问：怎么用属性选择器选？**
```HTML
<p class="first html">
My first html paragraph.
</p>
```

```CSS
p[class="first html"] {color: red;}
p[class~="html"] {color: red;}
```

CSS 选择器参考手册
选择器 | 描述
[attribute] | 用于选取带有指定属性的元素。
[attribute=value] | 用于选取带有指定属性和值的元素。
[attribute~=value] | 用于选取属性值中包含指定词汇的元素。
[attribute|=value] | 用于选取带有以指定值开头的属性值的元素，该值必须是整个单词。
[attribute^=value] | 匹配属性值以指定值开头的每个元素。
[attribute$=value] | 匹配属性值以指定值结尾的每个元素。
[attribute*=value] | 匹配属性值中包含指定值的每个元素。

### 后代选择器
选择作为某元素后代的元素。
```HTML
<ul type="square">
    <li id="coffee">Coffee</li>
        <ul class="classification">
            <li><em>Black</em> Coffee</li>
            <li>White Coffee</li>
        </ul>
    <li>Tea</li>
    <li>Milk</li>
</ul>
```
```CSS
ul em {background:black;}
```
*有关后代选择器有一个易被忽视的方面，即两个元素之间的层次间隔可以是无限的。*

### 子元素选择器
只能选择作为某元素子元素的元素。
```HTML
<h1>This is <strong>very</strong> <strong>very</strong> important.</h1>
<h1>This is <em>really <strong>very</strong></em> important.</h1>
```
```CSS
h1 > strong {color:red;}

/*refer to 后代选择器HTML*/
ul.classification li > em {background:black;}
```

### 相邻兄弟选择器
可选择紧接在另一元素后的元素，且二者有相同父元素。
```HTML
<ul type="square">
    <li>Coffee</li>
    <li>Tea</li>
    <li>Milk</li>
</ul>

<ol type="i">
    <li>Apple</li>
    <li>Pen</li>
    <li>Apple Pen
        <ul>
            <li>Orange Pen</li>
            <li>Strawberry Pen</li>
        </ul>
    </li>
</ol>
```
```CSS
/*选择紧接在li元素后出现的列表，第一个li和第二个li元素拥有共同的父元素*/
li + li {font-weight:bold;}
```

### 伪类
```CSS
a:link {color: #FF0000}		/* 未访问的链接 */
a:visited {color: #00FF00}	/* 已访问的链接 */
a:hover {color: #FF00FF}	/* 鼠标移动到链接上 */
a:active {color: #0000FF}	/* 选定的链接 */
li:first-child {text-transform:uppercase;}	/* li的第一个子元素 */
input:focus
{
background-color:yellow;    /* 获取焦点时背景色 */
}
q:lang(no)
   {
   quotes: "~" "~"          /* 为属性值为no的q元素定义引号的类型 */
   }
```

### 伪元素
```CSS
p:first-line                /* p的首行 */
  {
  color:#ff0000;
  font-variant:small-caps;
  }
p:first-letter              /* p的首字符 */
  {
  color:#ff0000;
  font-size:xx-large;
  }
h1:before
  {
  content:url(logo.gif);    /* 子在每个h1元素前插入logo */
  }
h1:after
  {
  content:url(logo.gif);    /* 子在每个h1元素后插入logo */
  }
```