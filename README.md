#### 查找形如 0,234,3431 的字符串 
```
^0,\d{1,10},\d{1,10}
```


#### 查找 hi 这个单词
```
\b
```

#### 查找 hi 后面不远处跟着一个 Lucy
```
\bhi\b.*\bLucy\b
```
* .是另一个元字符，匹配除了换行符以外的任意字符
* 而 * 同样是元字符，不过它代表的不是字符，也不是位置，而是数量——它指定*前边的内容可以连续重复使用任意次以使整个表达式得到匹配。
* 因此，.* 连在一起就意味着任意数量的不包含换行的字符

#### 查找一位数字
```
\d
```
#### 查找形如 023-90892361 的字符串
```
0\d{2}-\d{8}。
```

#### 匹配以字母a开头的单词
```
\ba\w*\b
```
* \w 任意一个字母或数字

#### 刚好6个字符的单词。
```
\b\w{6}\b
```

#### QQ号必须为5位到12位数字
```
^\d{5,12}$
```
* ^	匹配字符串的开始
* $	匹配字符串的结束

#### 字符转义
> 如果你想查找元字符本身的话，比如你查找.,或者*,就出现了问题：你没办法指定它们，因为它们会被解释成别的意思。这时你就得使用\来取消这些字符的特殊意义。因此，你应该使用\.和\*。当然，要查找\本身，你也得用\\.

* 匹配 deerchao.cn
```
deerchao\.cn
```
* 匹配C:\Windows
```
C:\\Windows
```

#### 匹配Windows后面跟1个或更多数字
```
Windows\d+
```
* + 重复一次或更多次
* ? 重复零次或一次

#### 任何一个英文元音字母
```
[aeiou]
```
> 要想查找数字，字母或数字，空白是很简单的，因为已经有了对应这些字符集合的元字符，但是如果你想匹配没有预定义元字符的字符集合(比如元音字母a,e,i,o,u),应该怎么办？很简单，你只需要在方括号里列出它们

#### 匹配几种格式的电话号码，像(010)88886666，或022-22334455，或02912345678等
```
\(?0\d{2}[) -]?\d{8}
```
我们对它进行一些分析吧：首先是一个转义字符\(,它能出现0次或1次(?),然后是一个0，后面跟着2个数字(\d{2})，然后是)或-或空格中的一个，它出现1次或不出现(?)，最后是8个数字(\d{8})。

#### IP地址匹配
```
(\d{1,3}\.){3}\d{1,3}
```
* \d{1,3}匹配1到3位的数字，(\d{1,3}\.){3}匹配三位数字加上一个英文句号(这个整体也就是这个分组)重复3次
* 这里由于涉及到 . 的查找，所以使用了字符转义 \.

#### 匹配两种以连字号分隔的电话号码：一种是三位区号，8位本地号(如010-12345678)，一种是4位区号，7位本地号(0376-2233445)。
```
0\d{2}-\d{8}|0\d{3}-\d{7}
```
* 正则表达式里的分枝条件指的是有几种规则，如果满足其中任意一种规则都应该当成匹配，具体方法是用|把不同的规则分隔开。

#### 美国邮编:5位数字，或者用连字号间隔的9位数字
```
\d{5}-\d{4}|\d{5}
```
之所以要给出这个例子是因为它能说明一个问题：使用分枝条件时，要注意各个条件的顺序。如果你把它改成\d{5}|\d{5}-\d{4}的话，那么就只会匹配5位的邮编(以及9位邮编的前5位)。原因是匹配分枝条件时，将会从左到右地测试每个条件，如果满足了某个分枝的话，就不会去再管其它的条件了。

#### 反义
* 匹配不包含空白符的字符串
```
\S+
```
* \W	匹配任意不是字母，数字，下划线，汉字的字符
* \S	匹配任意不是空白符的字符
* \D	匹配任意非数字的字符
* \B	匹配不是单词开头或结束的位置
* [^x]	匹配除了x以外的任意字符
* [^aeiou]	匹配除了aeiou这几个字母以外的任意字符
---
 
```
(\.\.\/)+image
```
匹配 
```
../image

../../image

../../../image
```
---
* 去掉所有 console.log(XXXX)
```
console.log(.*)
```
---
* 正则替换：保留原先部分内容
> [参考](http://122.51.66.78/article/5efdd5705c1b6d299c341833)
我想把
```
1. 适用范围
...
2. 信息使用
...
3. 信息安全
```
变成
```
<view class="head">1. 适用范围</view>
...
<view class="head">2. 信息使用</view>
...
<view class="head">3. 信息安全</view>
```
* 方法
```
(\d).([\u4e00-\u9fa5]+)

<view class="head">$1.$2</view>
```
其中
1. $1 表示正则表达式中第一个括号内的内容，$2 同理
2. [\u4e00-\u9fa5] 表示匹配一个汉字，[\u4e00-\u9fa5]+ 表示匹配多个连续的汉字（不限定个数）

