<br/>
<p align="center">
<img src="https://i.imgur.com/bYwl7Vf.png" alt="Learn Regex">
</p><br/>

## 何为正则表达式?
> 正则表达式是用来从文本中查找符合特定规则的字符串的一组字符或符号.

一个正则表达式被称为一个模式,为了从左到右匹配一系列目标字符串."Regular expression" 是个比较口头的称呼,通常你会将术语缩写成  "regex" 或者 "regexp".正则表达式不只可以用来替换一段文本中的字符,验证表单,根据匹配模式从字符串中提取字符,等等.

想想如果你正在写一个用户管理的应用, 接着你想要给用户名设定一系列的限制.比如,用户名可以
包含字母，数字，下划线和连字,但是有字数限制.
这样,我们就可以用下图的正则表达式来验证用户名的合法性:

<p align="center">
<img src="https://i.imgur.com/UrDb9qc.png" alt="Regular expression">
</p>

上面的正则表达式可以匹配像 `john_doe`,`jo-hn\_doe`,`john12\_as` 这样的用户名.但是不能匹配 `Jo` ,因为它包含大写字母,而且也太短了.

## 目录

- [基本语法](#1-基本语法)
- [元字符](#2-元字符)
  - [句点](#21-句点)
  - [字符集合](#22-字符集合)
    - [排除型字符集合](#221-排除型字符集合)

## 1. 基本语法

一个正则表达式就是有字母和数字组成的"模式",我们用它来搜索一段文本.举个例子,`cat` 这个正则表达式表示:字母 `c` ,接着是 `a` ,再接着 `t`.

<pre>
"cat" => The <a href="#learn-regex"><strong>cat</strong></a> sat on the mat
</pre>

正则表达式 `123` 匹配字符串"123".正则表达式将表达式中的每个字符和输入的每个字符逐个比较,来进行匹配的.正则表达式一般是大小写敏感的.所以表达式 `Cat` 不能匹配"cat".

 <pre>
"Cat" => The cat sat on the <a href="#learn-regex"><strong>Cat</strong></a>
</pre>

## 2. 元字符

可以说元字符是构成正则表达式的"砖块". 元字符不单独出现,但可以以特殊的方式插入.一些有特殊含义的元字符会被写在方括号内.
下面是元字符的表格:
|元字符|描述|
|:----:|----|
|.|匹配除"\n"以外的任意字符.|
|[ ]|字符集合(Character class).匹配方括号所包含的任意一个字符.|
|[^ ]|排除型 字符集合(Negated character class).匹配方括号不包含的任意一个字符.|
|*|匹配前面的子表达式零次或多次.|
|+|匹配前面的子表达式一次或多次.|
|?|使前面的子表达式可选|
|{n,m}|大括号.前面的子表达式最少匹配n次,最多匹配m次.|
|(xyz)|字符组(Character group).按**顺序**匹配字符串"xyz".|
|x&#124;y|匹配x或y.|
|&#92;|将下一个字符标记为特殊字符.这可以用来匹配保留的字符: <code>[ ] ( ) { } . * + ? ^ $ \ &#124;</code>|
|^|匹配输入字符串的开始位置|
|$|匹配输入字符串的结束位置|

## 2.1 句点

句点 `.` 是元字符中最简单的. 句点 `.` 匹配任意一个字符.但是**不会匹配"\n"**(换行符).比如说这个正则表达式 `.ar` 代表:任意的含有"ar"的字符串.

<pre>
".ar" => The <a href="#learn-regex"><strong>car</strong></a> <a href="#learn-regex"><strong>par</strong></a>ked in the <a href="#learn-regex"><strong>gar</strong></a>age.
</pre>

## 2.2 字符集合
字符集合也可以翻译成字符类(个人感觉还是字符集合比较符合它的特征).方括号 `[ ]` 用来指定字符集合,使用连字符可以指定字符范围.方括号内的字符顺序不重要.比如下面这个表达式 `[Tt]he` 表示:一个大写的 `T`或者是 小写的 `t` 接下来是 `h` ,再是 `e`.

<pre>
"[Tt]he" => <a href="#learn-regex"><strong>The</strong></a> car parked in <a href="#learn-regex"><strong>the</strong></a> garage.
</pre>

然而一个方括号内的句点 `[.]`,表示匹配句点.比如正则表达式 `ar[.]` 代表一个 `a` ,接着是 `r`,再是一个 `.` 的符号.

<pre>
"ar[.]" => A garage is a good place to park a c<a href="#learn-regex"><strong>ar.</strong></a>
</pre>

### 2.2.1 排除型字符集合

本来元字符 `^` 表示输入字符的开始位置.但是当她在方括号内时她会排除字符集合内的字符.比如 `[^c]ar` 这个表达式,就表示:任意的除了 `c` 意外的字符,接着是 `a`,再接着是 `r`.

<pre>
"[^c]ar" => The car <a href="#learn-regex"><strong>par</strong></a>ked in the <a href="#learn-regex"><strong>gar</strong></a>age.
</pre>

## 2.3 重复

`+`,`*` 和 `?` 这几个元字符用来表示一个子表达式可以重复的次数.但是这些元字符在不同情况下有不同的含义.

### 2.3.1 星号



### 2.3.2
### 2.3.3
## 2.4
## 2.5
## 2.6
## 2.7
## 2.8
### 2.8.1
### 2.8.2

## 3.

## 4.
### 4.1
### 4.2
### 4.3
### 4.4

## 5.
### 5.1
### 5.2
### 5.3

## Bonus

## Contribution

## License