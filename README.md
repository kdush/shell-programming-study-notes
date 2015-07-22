#shell编程学习笔记

####作者  *类星体* 
[![Smaller icon]( https://assets-cdn.github.com/images/modules/logos_page/GitHub-Mark.png =24x24)](https://github.com/kdush)  
[![Smaller icon]( http://www.sinaimg.cn/blog/developer/wiki/LOGO_24x24.png "Title here")](http://weibo.com/u/1080552231) 


##变量

####变量名

	1. 首个字符必须为字母（a-z，A-Z） 或者_
	2. 中间不能有空格，可以使用下划线（_）
	3. 不能使用其他标点符号
	
####变量赋值

```
a=123
b=$a
 
```
####变量取值
shell里也有特殊字符。常见的有美元符号 $ 反斜线 \ 和单引号 '' 与双引号 ""。

```
c=$a+$b
echo $c
```
*输出结果*

```
123+123
```
由双引号括起来的字符，除$，倒引号 ` 和反斜线 \ 仍保留其特殊功能外，其余字符均作为普通字符对待

由倒引号括起来的字符串被shell解释为命令行，在执行时，shell会先执行该命令，并以它的标准输出结果取代整个引号部分。

```
echo "$a 是变量a `pwd`是当前路径  \$c是变量c"
```

*输出结果*

```
123 是变量a /Users/ray/shelldemo是当前路径  $c是变量c"
```

由单引号括起来的字符都作为普通字符出现。

```
echo '$a 是变量a `pwd`是当前路径  \$c是变量c'
```

*输出结果*

```
$a 是变量a `pwd`是当前路径  \$c是变量c
```


###特殊变量

变量名 | 说明 
------|------
$$|当前进程PID
$0|当前脚本的文件名
$n|对应调用本脚本的参数,n是十进制数字,1是第一个参数,2是第二个参数
$#|调用当前脚本的参数个数
$*|调用当前脚本的所有参数组成一个参数
$@|同上 差异下面解释
$?|命令退出时的执行状态,可以理解为返回值
$!|最后一个命令的进程号


_对$@和$*差异的个人理解_

$ * 所有的位置参数,被作为一个单词 注意:$ * 必须被""引用 <br />

$@与$*同义,但是每个参数都是一个独立的""引用字串,这就意味着参数被完整地传递,
并没有被解释和扩展.也就是说,每个参数列表中的每个参数都被当成一个独立的单词.注意:"$@"必须被引用.


```
shell中运行
sh test.sh  aaa bbb 

 #!/bin/bash
 
	echo $*

	echo $@

	echo "$*"

	echo "$@"
 ```
_输出结果_

```
aaa bbb
aaa bbb
aaa bbb
aaa bbb
```


$@ $ * 只在被双引号包起来的时候才会有差异
$*将所有的参数认为是一个字段
$@以IFS（默认为空格）来划分字段，如果空格在“”里面，不划分。采用LS的脚本运行./test 1 "2 3" 4   来发现差异

没有括起来的情况是$@和$*一样的，见到IFS就划分字段。还是采用LS的脚本运行./test 1 "2 3" 4   来发现差异

 ```
shell中运行
sh test.sh 1 "2 3 " 4

 #!/bin/bash
 
	echo $*

	echo $@

	echo "$*"

	echo "$@"
 ```

_输出结果_

```
1 2 3 4
1 2 3 4
1 2 3  4
1 2 3  4
```

##比较运算

###比较运算符

```
lg 大于  >
lt 小于  <
eq 等于  ==
neq 不等于  !=
```

###数字比较

