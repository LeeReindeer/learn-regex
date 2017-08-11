<br/>
<p align="center">
<img src="https://i.imgur.com/bYwl7Vf.png" alt="Learn Regex">
</p><br/>

Translate by [Lee](https://github.com/LeeReindeer).
翻译水平有限，如有谬误，欢迎评论改正或者Pull Request.

[原文地址](https://github.com/zeeshanu/learn-regex)

## 何为正则表达式?
> 正则表达式是用来从文本中查找符合特定规则的字符串的一组字符或符号.

一个正则表达式被称为一个模式,为了从左到右匹配一系列目标字符串."Regular expression" 是个比较口头的称呼,通常你会将术语缩写成  "regex" 或者 "regexp".正则表达式不只可以用来替换一段文本中的字符,验证表单,根据匹配模式从字符串中提取字符,等等.

想想如果你正在写一个用户管理的应用, 接着你想要给用户名设定一系列的限制.比如,用户名可以
包含字母，数字，下划线和连字,但是有字数限制.
这样,我们就可以用下图的正则表达式来验证用户名的合法性:

<p align="center">
<img src="https://i.imgur.com/UrDb9qc.png" alt="Regular expression">
</p>

上面的正则表达式可以匹配像 `john_doe`,`jo-hn_doe`,`john12_as` 这样的用户名.但是不能匹配 `Jo` ,因为它包含大写字母,而且也太短了.

## 目录

- [基本语法](#1-基本语法)
- [元字符](#2-元字符)
  - [句点](#21-句点)
  - [字符集合(Character class)](#22-字符集合)
    - [排除型字符集合](#221-排除型字符集合)
  - [重复符号](#23-重复符号)
    - [星号](#231-星号)
    - [加号](#232-加号)
    - [问号](#233-问号)
  - [大括号](#24-大括号)
  - [或](#25-或)
  - [字符组(Character group)](#26-字符组)
  - [反斜杠](#27-反斜杠)
  - [锚(Anchors)](#28-锚)
    - [插入符号](#281-插入符号)
    - [美元符号](#282-美元符号)
- [缩写字符集合](#3-缩写字符集合)
- [正反向预查](#4-正反向预查)
  - [正向肯定预查](#41-正向肯定预查)
  - [正向否定预查](#42-正向否定预查)
  - [反向肯定预查](#43-反向肯定预查)
  - [反向否定预查](#44-反向否定预查)
- [标志](#5-标志)
  - [大小写不敏感](#51-大小写不敏感)
  - [全局搜索](#52-全局搜索)
  - [多行匹配](#53-多行匹配)
- [实例@^@](#实例)

## 1. 基本语法

一个正则表达式就是有字母和数字组成的"模式",我们用它来搜索一段文本.举个例子,`cat` 这个正则表达式表示:字母 `c` ,接着是 `a` ,再接着 `t`.

<pre>
"cat" => The <a href="#learn-regex"><strong>cat</strong></a> sat on the mat
</pre>

[测试一下](https://regex101.com/r/FOq5Nb/1)

正则表达式 `123` 匹配字符串"123".正则表达式将表达式中的每个字符和输入的每个字符逐个比较,来进行匹配的.正则表达式一般是大小写敏感的.所以表达式 `Cat` 不能匹配"cat".

 <pre>
"Cat" => The cat sat on the <a href="#learn-regex"><strong>Cat</strong></a>
</pre>

[测试一下](https://regex101.com/r/jw4Vi6/1)

## 2. 元字符

可以说元字符是构成正则表达式的"砖块". 元字符不单独出现,但可以以特殊的方式插入.一些有特殊含义的元字符会被写在方括号内.
下面是元字符的表格:

| 元字符 | 描述 |
|--------|--------|
|.       |匹配除"\n"以外的任意字符.|
|[ ]     |字符集合(Character class).匹配方括号所包含的任意一个字符.|
|[^ ] |排除型字符集合(Negated character class).匹配方括号不包含的任意一个字符.|
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

[测试一下](https://regex101.com/r/xc9GkU/1)

## 2.2 字符集合
字符集合也可以翻译成字符类(个人感觉还是字符集合比较符合它的特征).方括号 `[ ]` 用来指定字符集合,使用连字符可以指定字符范围.方括号内的字符顺序不重要.比如下面这个表达式 `[Tt]he` 表示:一个大写的 `T`或者是 小写的 `t` 接下来是 `h` ,再是 `e`.

<pre>
"[Tt]he" => <a href="#learn-regex"><strong>The</strong></a> car parked in <a href="#learn-regex"><strong>the</strong></a> garage.
</pre>

[测试一下](https://regex101.com/r/2ITLQ4/1)

然而一个方括号内的句点 `[.]`,表示匹配句点.比如正则表达式 `ar[.]` 代表一个 `a` ,接着是 `r`,再是一个 `.` 的符号.

<pre>
"ar[.]" => A garage is a good place to park a c<a href="#learn-regex"><strong>ar.</strong></a>
</pre>

[测试一下](https://regex101.com/r/wL3xtE/1)

### 2.2.1 排除型字符集合

本来元字符 `^` 表示输入字符的开始位置.但是当她在方括号内时她会排除字符集合内的字符.比如 `[^c]ar` 这个表达式,就表示:任意的除了 `c` 意外的字符,接着是 `a`,再接着是 `r`.

<pre>
"[^c]ar" => The car <a href="#learn-regex"><strong>par</strong></a>ked in the <a href="#learn-regex"><strong>gar</strong></a>age.
</pre>

[测试一下](https://regex101.com/r/nNNlq3/1)

## 2.3 重复符号

`+`,`*` 和 `?` 这几个元字符用来表示一个子表达式可以重复的次数.但是这些元字符在不同情况下有不同的含义.

### 2.3.1 星号
星号 `*` 表示匹配前面的子表示零次或多次.比如,正则表达式 `a*` 代表:匹配小写字母 `a` 零次或多次.但是当她出现在字符集合的后面时,她会匹配字符集合中的任意字符.比如 `[a-z]*` 代表:匹配任意的小写字母.

<pre>
"[a-z]*" => T<a href="#learn-regex"><strong>he</strong></a> <a href="#learn-regex"><strong>car</strong></a> <a href="#learn-regex"><strong>parked</strong></a> <a href="#learn-regex"><strong>in</strong></a> <a href="#learn-regex"><strong>the</strong></a> <a href="#learn-regex"><strong>garage</strong></a> #21.
</pre>

[测试一下](https://regex101.com/r/7m8me5/1)

星号 `*` 还可以和元字符 `.` 组合成 `.*` 来匹配任意的字符串.也可以和空格符 `\s` 组合来匹配一连串的空格.比如表达式 `\s*cat\s*` 代表零个或多个空格,接下来是 小写字母 `c` ,接下来是 `a` ,接下来是 `t` ,再接下来又是零个或多个的空格.

<pre>
"\s*cat\s*" => The fat<a href="#learn-regex"><strong> cat </strong></a>sat on the <a href="#learn-regex"><strong>cat</strong></a>.
</pre>

[测试一下](https://regex101.com/r/gGrwuz/1)

### 2.3.2 加号

加号 `+` 匹配前面的子表达式一次或多次.比如下面这个表达式 `c.+t` 表示一个 `c` ,接着可以是任意数目的任意字符,再接着是 `t`.

<pre>
"c.+t" => The fat <a href="#learn-regex"><strong>cat sat on the mat</strong></a>.
</pre>

[测试一下](https://regex101.com/r/Dzf9Aa/1)

### 2.3.3 问号

元字符 `?` 可以使前面的子表达式变成可选项.就是相当于匹配前面的子表达式零次或者一次.比如正则表达式 `[T]?th` 代表:可选的 大写字母 `T` ,接着是 `h` ,再是 `e` .

<pre>
"[T]he" => <a href="#learn-regex"><strong>The</strong></a> car is parked in the garage.
</pre>
<pre>
"[T]?he" => <a href="#learn-regex"><strong>The</strong></a> car is parked in t<a href="#learn-regex"><strong>he</strong></a> garage.
</pre>

[测试一下](https://regex101.com/r/cIg9zm/1)

## 2.4 大括号

在正则表达式中，大括号也称为量词，用于指定一组字符或一个字符可以重复的次数。比如表达式 `[0-9]{2,3}` 表示:匹配2到3个数字.如果去掉逗号的话,比如 `[0-9]{3}` 表示匹配3个数字.

<pre>
"[0-9]{2,3}" => The number was 9.<a href="#learn-regex"><strong>999</strong></a>7 but we rounded it off to <a href="#learn-regex"><strong>10</strong></a>.0.
</pre>

[测试一下](https://regex101.com/r/juM86s/1)

我们可以略去第二个数字.比如表达式 `[0-9]{2,}` 表示:匹配2个及以上个数字.

<pre>
"[0-9]{2,}" => The number was 9.<a href="#learn-regex"><strong>9997</strong></a> but we rounded it off to <a href="#learn-regex"><strong>10</strong></a>.0.
</pre>

[测试一下](https://regex101.com/r/Gdy4w5/1)

<pre>
"[0-9]{3}" => The number was 9.<a href="#learn-regex"><strong>99</strong></a><a href="#learn-regex"><strong>9</strong></a>7 but we rounded it off to 10.0.
</pre>

[测试一下](https://regex101.com/r/gqajq8/1)

## 2.5 或

正则表达式中,用 竖直条 `|` 表示逻辑或,她就像表达式之间的条件.现在你或许在想这不是和字符集合一样吗?但是她们之间的巨大差异是字符集合在字符级别的,而 `|` 在表达式级别.比如表达式 `(T|t)he|car` 表示:大字母 `T` 或是 `t`,接下来是 `h` 和 `e`.或者也可以匹配小写字母 `c`,接着是 `a` ,再接着是 `r` .

<pre>
"(T|t)he|car" => <a href="#learn-regex"><strong>The</strong></a> <a href="#learn-regex"><strong>car</strong></a> is parked in <a href="#learn-regex"><strong>the</strong></a> garage.
</pre>

[测试一下](https://regex101.com/r/fBXyX0/1)

## 2.6 字符组

字符组(Character group,注意与字符集合(Character class的区别))是一组写在圆括号 `(...)` 内的子表达式.上面已经讨论过,如果我们把表示重复的元字符(`*` `+` `?`)放在字符之后,她表示前面的字符重复若干次.但是当我们把它们放在字符组后面时,她表示重复整个字符组.比如 `(ab)*` 这个正则表达式匹配零次或多次字符串"ab".我们也可以把 `|` 放进字符组.比如 `(c|g|p)ar` 代表:小写字母 `c`,或 `g` ,或 `p` ,接着是 `a` 和 `r` .

<pre>
"(c|g|p)ar" => The <a href="#learn-regex"><strong>car</strong></a> is <a href="#learn-regex"><strong>par</strong></a>ked in the <a href="#learn-regex"><strong>gar</strong></a>age.
</pre>

[测试一下](https://regex101.com/r/tUxrBG/1)

## 2.7 反斜杠

反斜杠 `\` 在正则表达式中用来对元字符 `{ } [ ] / \ + * . $ ^ | ?` 进行转义.把 `\` 作为前缀来使用转义字符.比如 `.` 本来表示匹配任意字符,除了换行符.现在这个例子则不同.`(f|c|m)at.\?` 表示 `f` 或 `c` 或是 `m` 接下来是 `a` 和 `t`,再接着是可选的 `.`(句号).

<pre>
"(f|c|m)at\.?" => The <a href="#learn-regex"><strong>fat</strong></a> <a href="#learn-regex"><strong>cat</strong></a> sat on the <a href="#learn-regex"><strong>mat.</strong></a>
</pre>

[测试一下](https://regex101.com/r/DOc5Nu/1)

## 2.8 锚

在正则表达式中,检查输入字符串匹配的最后的字符和第一个字符,我们使用锚(Anchors).锚分为两类:第一类是插入符号 `^` 检查输入字符串的开始位置;第二类是美元符号 `$` 用来检查输入字符串的结束位置.

### 2.8.1 插入符号

插入符号 `^` 用来检查输入字符串的开始位置.如果我们使用下面的表达式 `^a` (如果a是起始字符) 来匹配输入字符串 "abc" 她会匹配 `a` .但是如果使用 `^b` ,则不会匹配任何字符,因为"b"不是起始的字符.让我们来看看另一个正则表达式 `^(T|t)he` ,她表示:`T` 或 `t` 是起始的字符,接着是 `h` 和 `e` .

<pre>
"(T|t)he" => <a href="#learn-regex"><strong>The</strong></a> car is parked in <a href="#learn-regex"><strong>the</strong></a> garage.
</pre>

[测试一下](https://regex101.com/r/5ljjgB/1)

<pre>
"^(T|t)he" => <a href="#learn-regex"><strong>The</strong></a> car is parked in the garage.
</pre>

[测试一下](https://regex101.com/r/jXrKne/1)

### 2.8.2 美元符号

美元符号 `$` 用来匹配输入字符串的结束位置.比如表达式 `(at\.)$` 表示 `a` 和 `t`, 接着是一个句号 `.`,句号必须是结尾.

<pre>
"(at\.)" => The fat c<a href="#learn-regex"><strong>at.</strong></a> s<a href="#learn-regex"><strong>at.</strong></a> on the m<a href="#learn-regex"><strong>at.</strong></a>
</pre>

[测试一下](https://regex101.com/r/y4Au4D/1)

<pre>
"(at\.)$" => The fat cat. sat. on the m<a href="#learn-regex"><strong>at.</strong></a>
</pre>

https://regex101.com/r/t0AkOd/1

## 3. 缩写字符集

正则表达式为常用的字符集合提供了缩写.缩写的字符集如下:

|缩写|描述|
|:----:|----|
|.|匹配除"\n"外的任意字符|
|\w|匹配字母和数字: `[a-zA-Z0-9_]`|
|\W|匹配子母河数字以外的字符: `[^\w]`|
|\d|匹配数字: `[0-9]`|
|\D|匹配数字以外的字符: `[^\d]`|
|\s|匹配空格字符: `[\t\n\f\r\p{Z}]`|
|\S|匹配空格以外的字符: `[^\s]`|

## 4. 正反向预查

正向和反向预查是特殊的一类非获取匹配(***non-capturing group***,用来匹配子表达式但是不包含在匹配列表内.)正反向预查会检查一个子表达式在另一个子表达式之后或之前.比如我们想要从这个字符串 `$4.44 and $10.88` 中获取美元符号 `$` 之后的所有数字,我们可以使用这个表达式 `(?<=\$)[0-9\.]*` .她表示:匹配所有包含 `.` 和以 `$` 为前缀的数字.
下面是所有的正反向预查:

|符号|描述|
|:----:|----|
|?=|正向肯定预查|
|?!|正向否定预查|
|?<=|反向肯定预查|
|?<!|反向否定预查|

### 4.1 正向肯定预查

正向肯定预查表示表达式的第一部分接下来必须是正向肯定表达式(lookahead expression).返回的匹配必须只包含来自表达式的第一部分的字符.我们用 `(?=...)` 来表示正向肯定预查.正向肯定表达式写在被括号包含的等号后面.比如 `(T|t)he(?=\sfat)` 代表:`T` 或 `t` 接着是 `h` 和 `e` .正向肯定预查的作用就是保证 `The` 或 `the` 接下来是 空格+`fat`.

 <pre>
"(T|t)he(?=\sfat)" => <a href="#learn-regex"><strong>The</strong></a> fat cat sat on the mat.
</pre>

[测试一下](https://regex101.com/r/apqJZq/1)

### 4.2 正向否定预查

正向否定预查用来从输入字符串匹配那些字符接下来的字符是不匹配这个表达式的.正向否定预查的表示方法和正向肯定预查差不多,只是把 `=` 换成 `!` ,变成了 `(?!...)` .让我们来看看下面这个正则表达式 `(T|t)he(?!\sfat)`,她代表:匹配所有不跟着 空格+`fat` 的 `The` 或 `the`.

<pre>
"(T|t)he(?!\sfat)" => The fat cat sat on <a href="#learn-regex"><strong>the</strong></a> mat.
</pre>

[测试一下](https://regex101.com/r/sswCvQ/1)

### 4.3 反向肯定预查

反向肯定预查用来匹配以符合反向肯定表达式的字符为前缀的字符.反向肯定预查用 `(?<=...)` 来表示.比如这个表达式 `(?<=(T|t)he\s)(fat|mat)` 表示匹配所有 以 `The` 或 `the` 为前缀的 `fat` 或 `mat` .

<pre>
"(?<=(T|t)he\s)(fat|mat)" => The <a href="#learn-regex"><strong>fat</strong></a> cat sat on the <a href="#learn-regex"><strong>mat</strong></a>.
</pre>

[测试一下](https://regex101.com/r/TZ8DOX/1/)

### 4.4 反向否定预查

反向否定预查用来匹配以不符合表达式的字符为前缀的字符.反向否定预查用 `(?<!...)` 来表示.比如 `(?&lt;!(T|t)he\s)(cat)` 表示匹配所有不以 `The` 或 `the` +空格 为前缀的 `cat` .

<pre>
"(?&lt;!(T|t)he\s)(cat)" => The cat sat on <a href="#learn-regex"><strong>cat</strong></a>.
</pre>

[测试一下](https://regex101.com/r/gleYg9/1)

## 5. 标志

标志也被称为修饰符，因为它们会改变正则表达式的输出.这些修饰符可以以任何顺序使用,并且是正则表达式的一部分.

|标志|描述|
|:----:|:----:|
|i|大小写不敏感: 将匹配设置为不区分大小写。|
|g|全局搜索: 搜索整个输入字符串|
|m|多行匹配: 使锚 `^,$` 在每一行上都有效。|

### 5.1 大小写不敏感

`i` 修饰符表现为不区分大写小的匹配.比如表达式 `/The/gi` 表示: `T`,接着 `h` ,接着 `e`.`i`的作用是让正则表达式忽略大小写.你可以看到我们也是用来修饰符 `g`,因为我们想要搜索整个输入的字符串.

<pre>
"The" => <a href="#learn-regex"><strong>The</strong></a> fat cat sat on the mat.
</pre>

[测试一下](https://regex101.com/r/dpQyf9/1)

<pre>
"/The/gi" => <a href="#learn-regex"><strong>The</strong></a> fat cat sat on <a href="#learn-regex"><strong>the</strong></a> mat.
</pre>

[测试一下](https://regex101.com/r/ahfiuh/1)

### 5.2 全局搜索

修饰符 `g` 可以进行全局搜索(找到所有符合的,而不是找到一个就停止).比如 `/.(at)/g` 表示除了"\n"的任何字符,接下来是 `at` 因为我们用来修饰符 `g` ,下载她会找到每一个匹配的字符串.

<pre>
".(at)" => The <a href="#learn-regex"><strong>fat</strong></a> cat sat on the mat.
</pre>

[测试一下](https://regex101.com/r/jnk6gM/1)

<pre>
"/.(at)/g" => The <a href="#learn-regex"><strong>fat</strong></a> <a href="#learn-regex"><strong>cat</strong></a> <a href="#learn-regex"><strong>sat</strong></a> on the <a href="#learn-regex"><strong>mat</strong></a>.
</pre>

[测试一下](https://regex101.com/r/dO1nef/1)

### 5.3 多行匹配

修饰符 `m` 可以用来进行多行匹配.我们之前说过的锚 `^,$` 是用来检查输入文本的开始位置和结束位置的.但是如果我们想要锚在每一行上都有效,我们就要使用 `m` 修饰符.比如表达式 `/at(.)?$/gm` 代表:`a` 接着是 `t`,再是一个可选的任意除换行符之外的字符.因为有修饰符 `m` ,所以正则表达式引擎会匹配每一行的末尾. 

<pre>
"/.at(.)?$/" => The fat
                cat sat
                on the <a href="#learn-regex"><strong>mat.</strong></a>
</pre>

[测试一下](https://regex101.com/r/hoGMkP/1)

<pre>
"/.at(.)?$/gm" => The <a href="#learn-regex"><strong>fat</strong></a>
                  cat <a href="#learn-regex"><strong>sat</strong></a>
                  on the <a href="#learn-regex"><strong>mat.</strong></a>
</pre>

[测试一下](https://regex101.com/r/E88WE2/1)

## 实例

- *正数*： `^\d+$`
- *负数*: `^-\d+$`
- *美国电话号码* `^+?[\d\s]{3,}$`
- *区号+美国电话* `^+?[\d\s]+(?[\d\s]{10,}$`
- *整数*: `^-?\d+$`
- *用户名*: `^[\w\d_.]{4,16}$`
- *字母和数字*: `^[a-zA-Z0-9]$`
- *带空格的字母数字*: `^[a-zA-Z0-9 ]$`
- *密码*: `^(?=^.{6,}$)((?=.*[A-Za-z0-9])(?=.*[A-Z])(?=.*[a-z]))^.*$`
- *邮箱*: `^([a-zA-Z0-9._%-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,4})*$`
- *IPv4地址*: `^((?:(?:25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?)\.){3}(?:25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?))*$`
- *小写字母*: `^([a-z])$` 
- *大写字母*: `^([A-Z])$` 
- *URL*: `^(((http|https|ftp):\/\/)?([[a-zA-Z0-9]\-\.])+(\.)([[a-zA-Z0-9]]){2,4}([[a-zA-Z0-9]\/+=%&_\.~?\-]*))*$`
- *日期(MM/DD/YYYY)*: `^(0?[1-9]|1[012])[- /.](0?[1-9]|[12][0-9]|3[01])[- /.]([12][0-9])?[0-9]{2}$` 
- *日期(YYYY/MM/DD)*: `^([12][0-9])?[0-9]{2}[- /.](0?[1-9]|1[012])[- /.](0?[1-9]|[12][0-9]|3[01])$`
- *万事达信用卡号码*: `^(5[1-5][0-9]{14})*$`
- *VISA信用卡号码*: `^(4[0-9]{12}(?:[0-9]{3})?)*$` 
- *Hashtags*: Including hashtags with preceding text (abc123#xyz456) or containing white spaces within square brackets (#[foo bar]) : `\S*#(?:\[[^\]]+\]|\S+)`
- *@mentions*: `\B@[a-z0-9_-]+`
## License

MIT © [Zeeshan Ahmed](mailto:ziishaned@gmail.com)