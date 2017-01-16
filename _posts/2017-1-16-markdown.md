---
layout: post
title:  "Markdown语法"
tags:
categories:
---


### 标题显示

```
# 这是H1    ##这是H2   ###这是H3   ####这是H4   #####这是H5    ######这是H6
```

### 无序列表
星号* 加号+ 减号-

```
* red
* blue
* green
等同于
+ red
+ blue
+ green
也等同于
- red
- blue
- green
```

### 有序列表
 数字接着一个英文句点

```
1. red
2. blue
3. green
```

### 分隔线
你可以在一行中用三个以上的星号、减号、底线来建立一个分隔线，行内不能有其他东西

```
* * *
***
*****
- - -
--------------
```

### 链接
Markdown 支持两种形式的链接语法： 行内式和参考式两种形式 不管是哪一种，链接文字都是用 [方括号] 来标记 
要建立一个行内式的链接，只要在方块括号后面紧接着圆括号并插入网址链接即可，如果你还想要加上链接的 title 文字，只要在网址后面，用双引号把 title 文字包起来即可
参考式的链接是在链接文字的括号后面再接上另一个方括号，而在第二个方括号里面要填入用以辨识链接的标记：

```
This is [an example](http://example.com/ "Title") inline link.
[This link](http://example.net/) has no title attribute.
This is [an example][id] reference-style link.
```

### 强调
Markdown 使用星号（*）和底线（_）作为标记强调字词的符号，被 * 或 _ 包围的字词会被转成用 <em> 标签包围，用两个 * 或 _ 包起来的话，则会被转成 <strong>

```
*single asterisks*
_single underscores_
**double asterisks**
__double underscores__
```

### 图片
Markdown 使用一种和链接很相似的语法来标记图片，同样也允许两种样式： 行内式和参考式

```
![Alt text](/path/to/img.jpg)
![Alt text](/path/to/img.jpg "Optional title")
![Alt text][id]
[id]: url/to/image  "Optional title attribute"
```

### 自动链接
Markdown 支持以比较简短的自动链接形式来处理网址和电子邮件信箱，只要是用方括号包起来， Markdown 就会自动把它转成链接。一般网址的链接文字就和链接地址一样

```
<http://example.com/>
<address@example.com>
```

### 反斜杠
Markdown 可以利用反斜杠来插入一些在语法中有其它意义的符号，例如：如果你想要用星号加在文字旁边的方式来做出强调效果（但不用 <em> 标签），你可以在星号的前面加上反斜杠

```
\   反斜线
`   反引号
*   星号
_   底线
{}  花括号
[]  方括号
()  括弧
#   井字号
+   加号
-   减号
.   英文句点
!   惊叹号
```
