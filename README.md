<!doctype html>
<html>
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=yes">
<style>
h1,
h2,
h3,
h4,
h5,
h6,
p,
blockquote {
    margin: 0;
    padding: 0;
}
body {
    font-family: "Helvetica Neue", Helvetica, "Hiragino Sans GB", Arial, sans-serif;
    font-size: 13px;
    line-height: 18px;
    color: #737373;
    background-color: white;
    margin: 10px 13px 10px 13px;
}
table {
	margin: 10px 0 15px 0;
	border-collapse: collapse;
}
td,th {	
	border: 1px solid #ddd;
	padding: 3px 10px;
}
th {
	padding: 5px 10px;	
}

a {
    color: #0069d6;
}
a:hover {
    color: #0050a3;
    text-decoration: none;
}
a img {
    border: none;
}
p {
    margin-bottom: 9px;
}
h1,
h2,
h3,
h4,
h5,
h6 {
    color: #404040;
    line-height: 36px;
}
h1 {
    margin-bottom: 18px;
    font-size: 30px;
}
h2 {
    font-size: 24px;
}
h3 {
    font-size: 18px;
}
h4 {
    font-size: 16px;
}
h5 {
    font-size: 14px;
}
h6 {
    font-size: 13px;
}
hr {
    margin: 0 0 19px;
    border: 0;
    border-bottom: 1px solid #ccc;
}
blockquote {
    padding: 13px 13px 21px 15px;
    margin-bottom: 18px;
    font-family:georgia,serif;
    font-style: italic;
}
blockquote:before {
    content:"\201C";
    font-size:40px;
    margin-left:-10px;
    font-family:georgia,serif;
    color:#eee;
}
blockquote p {
    font-size: 14px;
    font-weight: 300;
    line-height: 18px;
    margin-bottom: 0;
    font-style: italic;
}
code, pre {
    font-family: Monaco, Andale Mono, Courier New, monospace;
}
code {
    background-color: #fee9cc;
    color: rgba(0, 0, 0, 0.75);
    padding: 1px 3px;
    font-size: 12px;
    -webkit-border-radius: 3px;
    -moz-border-radius: 3px;
    border-radius: 3px;
}
pre {
    display: block;
    padding: 14px;
    margin: 0 0 18px;
    line-height: 16px;
    font-size: 11px;
    border: 1px solid #d9d9d9;
    white-space: pre-wrap;
    word-wrap: break-word;
}
pre code {
    background-color: #fff;
    color:#737373;
    font-size: 11px;
    padding: 0;
}
sup {
    font-size: 0.83em;
    vertical-align: super;
    line-height: 0;
}
* {
	-webkit-print-color-adjust: exact;
}
@media screen and (min-width: 914px) {
    body {
        width: 854px;
        margin:10px auto;
    }
}
@media print {
	body,code,pre code,h1,h2,h3,h4,h5,h6 {
		color: black;
	}
	table, pre {
		page-break-inside: avoid;
	}
}
</style>
<title>shell编程学习笔记</title>

</head>
<body>
<h1>shell编程学习笔记</h1>

<h4>作者  <em>类星体</em> <a href="https://github.com/kdush"><img src="https://assets-cdn.github.com/images/modules/logos_page/GitHub-Mark.png" height="24" width="24" alt="Smaller icon" /></a>  <a href="http://weibo.com/u/1080552231"><img src="http://www.sinaimg.cn/blog/developer/wiki/LOGO_24x24.png" title="Title here" alt="Smaller icon" /></a></h4>

<h2>变量</h2>

<h4>变量名</h4>

<pre><code>1. 首个字符必须为字母（a-z，A-Z） 或者_
2. 中间不能有空格，可以使用下划线（_）
3. 不能使用其他标点符号
</code></pre>

<h4>变量赋值</h4>

<pre><code>a=123
b=$a
</code></pre>

<h4>变量取值</h4>

<p>shell里也有特殊字符。常见的有美元符号 $ 反斜线 \ 和单引号 '' 与双引号 ""。</p>

<pre><code>c=$a+$b
echo $c
</code></pre>

<p><em>输出结果</em></p>

<pre><code>123+123
</code></pre>

<p>由双引号括起来的字符，除$，倒引号 ` 和反斜线 \ 仍保留其特殊功能外，其余字符均作为普通字符对待</p>

<p>由倒引号括起来的字符串被shell解释为命令行，在执行时，shell会先执行该命令，并以它的标准输出结果取代整个引号部分。</p>

<pre><code>echo "$a 是变量a `pwd`是当前路径  \$c是变量c"
</code></pre>

<p><em>输出结果</em></p>

<pre><code>123 是变量a /Users/ray/shelldemo是当前路径  $c是变量c"
</code></pre>

<p>由单引号括起来的字符都作为普通字符出现。</p>

<pre><code>echo '$a 是变量a `pwd`是当前路径  \$c是变量c'
</code></pre>

<p><em>输出结果</em></p>

<pre><code>$a 是变量a `pwd`是当前路径  \$c是变量c
</code></pre>

<h3>特殊变量</h3>

<table>
<thead>
<tr>
<th>变量名 </th>
<th> 说明</th>
</tr>
</thead>
<tbody>
<tr>
<td>$$</td>
<td>当前进程PID</td>
</tr>
<tr>
<td>$0</td>
<td>当前脚本的文件名</td>
</tr>
<tr>
<td>$n</td>
<td>对应调用本脚本的参数,n是十进制数字,1是第一个参数,2是第二个参数</td>
</tr>
<tr>
<td>$#</td>
<td>调用当前脚本的参数个数</td>
</tr>
<tr>
<td>$*</td>
<td>调用当前脚本的所有参数组成一个参数</td>
</tr>
<tr>
<td>$@</td>
<td>同上 差异下面解释</td>
</tr>
<tr>
<td>$?</td>
<td>命令退出时的执行状态,可以理解为返回值</td>
</tr>
<tr>
<td>$!</td>
<td>最后一个命令的进程号</td>
</tr>
</tbody>
</table>


<p><em>对$@和$*差异的个人理解</em></p>

<p>$ * 所有的位置参数,被作为一个单词 注意:$ * 必须被""引用 <br /></p>

<p>$@与$*同义,但是每个参数都是一个独立的""引用字串,这就意味着参数被完整地传递,
并没有被解释和扩展.也就是说,每个参数列表中的每个参数都被当成一个独立的单词.注意:"$@"必须被引用.</p>

<pre><code>shell中运行
sh test.sh  aaa bbb 

 #!/bin/bash

    echo $*

    echo $@

    echo "$*"

    echo "$@"
</code></pre>

<p><em>输出结果</em></p>

<pre><code>aaa bbb
aaa bbb
aaa bbb
aaa bbb
</code></pre>

<p>$@ $ * 只在被双引号包起来的时候才会有差异
$*将所有的参数认为是一个字段
$@以IFS（默认为空格）来划分字段，如果空格在“”里面，不划分。采用LS的脚本运行./test 1 "2 3" 4   来发现差异</p>

<p>没有括起来的情况是$@和$*一样的，见到IFS就划分字段。还是采用LS的脚本运行./test 1 "2 3" 4   来发现差异</p>

<pre><code>shell中运行
sh test.sh 1 "2 3 " 4

 #!/bin/bash

    echo $*

    echo $@

    echo "$*"

    echo "$@"
</code></pre>

<p><em>输出结果</em></p>

<pre><code>1 2 3 4
1 2 3 4
1 2 3  4
1 2 3  4
</code></pre>

<h2>比较运算</h2>

<h3>比较运算符</h3>

<pre><code>lg 大于  &gt;
lt 小于  &lt;
eq 等于  ==
neq 不等于  !=
</code></pre>

<h3>数字比较</h3>
</body>
</html>
 No newline at end of file
