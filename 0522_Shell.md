# shell script
本来是以前学过shell script的，但是好久没有写了，又不太记得大致的东西了，看来还是记录笔记很重要啊

## 第一个shell script
```
#!/bin/bash
echo "hello world"
```

 
## 然后改成可执行
` chmod 777 xxx`

## 如何写一个登陆脚本？
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