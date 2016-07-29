# shell script
本来是以前学过shell script的，但是好久没有写了，又不太记得大致的东西了，看来还是记录笔记很重要啊

## 第一个shell script
```
#!/bin/bash
echo "hello world"
```

 
## 然后改成可执行
` chmod 777 xxx`

## 下面是一本书的学习
### 准备工作
* 解释执行

### 数值运算
除了shell语法自带的几个运算，bc, expr, awk 命令都是被调用的存在/usr/bin下的命令
### 布尔运算
* && ||  前者表示第一个statement成立才会执行第二个statement, 后者表示一直执行到第一个成功的statement (不太确定)

### 字符串操作
### 文件操作
### 文件系统操作
### 进程操作
### 网络操作
### 总结

### 一些积累
* dirname string   删除string中最后一个`/`之后的内容
* `bash_source[0]`  几个参考 [1](http://stackoverflow.com/questions/421772/how-can-a-bash-script-know-the-directory-it-is-installed-in-when-it-is-sourced-w) [2](http://stackoverflow.com/questions/59895/can-a-bash-script-tell-which-directory-it-is-stored-in)
* set  [参考说明](http://linuxcommand.org/lc3_man_pages/seth.html)
* 

## 例子
### 如何写一个登陆脚本？
* 一种方法是使用public key登陆 见 [public](http://serverfault.com/questions/241588/how-to-automate-ssh-login-with-password) 
* 一个方案
使用sshpass 同上，但是 OSX 显然不会支持，因为不安全
* 使用expect 环境 （script支持交互式的一个程序）
	十分好的解释： [解释](https://www.centos.bz/2013/07/expect-spawn-linux-expect-usage/)
	1. `sudo brew install homebrew/dupes/expect`
	2. 然后开始写脚本    expect怎么用
	spawn 表示将要call 一个 命令 ；
	send表示匹配到一个返回时，发送的东西 
	interact 继续停留在远端，但是控制交给terminal 
	```
	#!/usr/bin/expect -f
 
	set timeout 10
	spawn ssh lixl@gw.cse.cuhk.edu.hk
	expect "assword"
	send "xxx\r"
	```
	但是，我还真的是没法再cuhk的home 来 spawn ssh...

## 参考教材 
[教材](http://tldp.org/LDP/abs/html/)
[一本书](http://www.tinylab.org/open-shell-book/)