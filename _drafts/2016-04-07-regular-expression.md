---
  layout: post
  title: 正则表达式
  tags:
  categories:
---

一句简单的话来概括:正则表达式本质上让我们拥有更强大的文本检索能力.
通过一些扩展函数,我们可以对检索到的结果做一些其他操作.
比如`构建程序数据`，`替换`，`拆分文本`等等.


## 测试工具

现在，我们来体验一下什么是 `更强大的文本检索能力`.
编辑器的搜索功能大家都很熟悉,
为了调试方便 chrome source 选项卡现在已经越来越像一个编辑器了,
在其中自然也有搜索替换功能,
同时也支持使用正则表达式来搜索.
界面如下:

![chrome调试工具 source选项卡界面](/blog/images/chrome-source.png)


## 可见原子

原子是正则表达式中的最小匹配单位,
通常为[Unicode编码表][unicode]中的一个字符,
我们把Unicode编码表中用键盘输出后肉眼可见的字符称为可见原子,
我们可以直接使用一个可见原子或多个可见原子的组合去目标字符串中查找文本,
就像普通的编辑器搜索.

简单罗列一下可见原子:

标点|字母|数字|汉字|其他
---|---|---|---|---
,|a|1|我|&
.|z|3|你|=
;|A|5|他|^
"|Z|8|它|$

在正则表达式中匹配汉字的时候我们最好把汉字转换成对应的UTF-8编码字符,以防止不同的文件编码带来的问题,
这里我们使用一个简单的函数 `chinese2utf8` 来进行转换

```javascript
// 10进制转16进制
var ten2hex = function (ten) {
  var _d = { 0: '0', 1: '1', 2: '2', 3: '3', 4: '4', 5: '5', 6: '6', 7: '7', 8: '8', 9: '9', 10: 'a', 11: 'b', 12: 'c', 13: 'd', 14: 'e', 15: 'f' };
  var r = [];
  do{
    r.push(_d[ ten % 16 ]);
    ten = parseInt(ten / 16);
  }while( ten )

  return r.reverse().join('');
}
var chinese2utf8 = function ( char ) {
  var str = '';
  for(var k in char ){
    var v = char[k];
    str += '\\u' + ten2hex( v.charCodeAt(0) );
  }
  return str;
}
```

当可见原子正好是正则表达式运算符时,
我们需要加上`\`进行转意.
正则表达式的运算符如下:



## 不可见原子

比如换行符,制表符等,
Atom编辑器有个配置选项可以让我们看到不可见字符,
这里有个截图

![一些不可见原子](/blog/images/invisible-atom.png)

途中灰色的部分就是一个不可见原子,分别代表空格和换行符,
正则表达式中使用一些特殊的形式来匹配不可见原子:

符号|匹配对象
-----------|-------------
` `|空格
\t|制表符
\n|换行符

## 元字符

由一些原子以正则表达式特有的规则组成的一个匹配单位

- `|`   匹配两个或多个分支选择
- `[]`  匹配方括号中的任意一个原子
- `[^]` 匹配除方括号中的原子之外的任意字符

正则表达式中预定了一些元字符集合,方便我们更好的使用

- .   除了换行符之外的任意字符
- \d  任意一个十进制数 `[0-9]`
- \D  任意一个非十进制数 `[^0-9]`
- \s  匹配一个不可见原子  `[\f\n\r\t\v]`
- \S  匹配一个可见原子    `[^\f\n\r\t\v]`
- \w  匹配一个数字,字母或下划线  `[0-9a-zA-Z_]`
- \W  匹配一个非数字,字母或下划线 `[^0-9a-zA-Z_]`
- \b  匹配单词边界

```javascript
var reg = /apple|google/;
var reg = /[a-zA-Z\s]/;
var reg = /[^0-9\t]/;
```

在`[]` 中 `-`字符表示从多少到多少  `a-z` 会把匹配所有的小写字母,
规则是按照Unicoe码从小到大的某个范围内

从元字符开始,正则表达式开始体现自己的优势,它不像简单的编辑器查找那样,只能找到特定的字符,
而是会找到符合某些逻辑规则的字符串集合,方便我们统一处理.

比如,我们可以把一个文件中的所有制表符都换成四个空格.

## 量词

只有元字符还不足以让正则表达式灵活到可以随意的匹配我们想要的文本.
搭配量词,正则表达式在智能匹配的道路上更进一步.

- `{n}`  表示其前面的原子恰好出现n次
- `{n,}` 表示其前面的原子最少出现n次
- `{n,m}` 表示其前面的原子最少出现n次,最多出现m次
- `*`   `{0,}`
- `+`   `{1,}`
- `?`   `{0,1}`

## 边界控制

- `^`   匹配字符串开始的位置  限制目标字符串必须以特定的规则开头
- `$`   匹配字符串结尾的位置  限制目标字符串必须以特定的规则结尾


## 模式单元

`( )` 匹配其中的整体为一个原子 非元字符

模式单元的作用非常强大,尤其是在处理替换类程序编程的时候,
下面我们看几个例子:





## 界定符

表示一个正则表达式的开始和结束位置,在javascript中

我们使用如下两种方式来定义一个正则表达式对象

```javascript
//1.字面量方式
var reg = /someregularexpression/;
//2.构造函数方式
var reg = new RegExp('/someregularexpression/',g);

var fn = function (x, y) {
  return x * y;
}
var num = fn(3, 4);
console.log(num);
```

其中位于 `someregularexpression` 两侧的 `/` 字符为界定符


[unicode]: http://blog.reigndesign.com/blog/love-hotels-and-unicode/
