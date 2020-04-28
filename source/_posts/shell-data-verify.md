---
title: shell data verify
date: 2020-04-28 13:41:31
tags:
---
最近转Linux,
学了一点shell script,
发现对拍程序可以这样写:

```shell
# data.out数据生成器,true.out对拍,ans.out要测试的程序
data.out|true.out > true.ans
data.out|ans.out > ans.ans
diff ans.ans true.ans
# -----
# 如果没有数据生成器
cat data.txt|true.out > true.ans
cat data.txt|ans.out > ans.ans
diff ans.ans true.ans
```
然后就可以实现对拍数据了

> 注:关于"`|`"管道操作符详见[这篇文章](https://afgxf.github.io/2020/04/27/Bash-Pipes/)

也可以写一个`test.sh`
```shell
$1|$2 > true.ans
$1|$3 > ans.ans
diff ans.ans true.ans
# -----
# 如果没有数据生成器
cat $1|$2 > true.ans
cat $1|$3 > ans.ans
diff ans.ans true.ans
```
然后可以通过`./test.sh 数据/生成器 对拍程序 要测试的程序`愉快的对拍了QWQ