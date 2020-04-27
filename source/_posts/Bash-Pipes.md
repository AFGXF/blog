---
title: Bash Pipes
date: 2020-04-27 12:34:42
tags:
    - Bash 
    - Shell Script
    - Linux
---
## 1. 它是什么
先看一组样例:
```bash
cat index.js|node|echo>>out.txt #其实就是node ./index.js>>out.txt
```
```bash
git log|echo>>history.log#保存log
```
```bash
find ./ xxx|sort #排序输出
```
## 2. 它怎么用
```bash
command1|command2[|commandN...]
```
将command1的stdout定向到command2的stdin,再将command2的stdout定向到command3的stdin,......

## 3. 用法
没有。

对。就是很没用。~~goto一般的存在~~有时还被斥责多余