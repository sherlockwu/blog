# Mininet 安装使用
这篇blog主要讲述Mininet的安装， 简介

## 安装
详见 [安装的官方说明](http://mininet.org/download/)
1. git clone   感觉git clone了好长时间
`git clone https://github.com/mininet/mininet.git`
2. 安装 
`/mininet/util/install.h -a`   当然还有几个可选项
中间 cloning into openflow 的时候会超时，尝试添加了 cuhk的 源 还是不行
应该是openflow的问题，它没有维护这个git server了 
`./install.h -nv` 可以，他没有安装openflow reference switch 
3. 结束

## mininet walkthrough   
本质上应该还只是个网络实验平台，应该提供 构建topo，设定各element，登陆各element的功能
wireshark本质上应该是一个从内核driver支持起来的app，所以应该可以运行在各switch和controller   这就是我大致设想的 mininet的功能

本质上 Mininet 是一个 VM 

### Everyday Mininet Usage
1. wireshark
	1. 安装`apt-get install wireshark` 
	2. 使用ssh提供的x11 GUI 共享功能 来 提供 wireshark 所需的 GUI （在ssh客户端显示）
	[参考简书的blog](http://www.jianshu.com/p/400d4430a74a)
	 
	3. 


### Advanced Startup Options
### Mininet CLI commands
### Python API Examples



## Reference
[安装的官方说明](http://mininet.org/download/)
