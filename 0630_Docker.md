# Docker 
## What is a docker? 
什么是docker？ 什么又是container? 

* Docker 使用go开发
* 分为两大部分: 
	* 资源管理: cgroup->LXC(libcontainer)->Docker
		* 实现了对于file system, network等的分配/ 隔离
		* 所以container实际上是基于 guest OS kernel的一种vir tech.， 并没有去virtualize 某OS的实现
			* 每个运行的容器只是 host OS中的一个进程， 然后docker中的程序也是一个进程，只不过和父docker处在一个group中
			* 一个图片 
			![docker_1](./images/docker_1.jpg)
		* 为什么不直接用 cgroup? 
			如果对同一台服务上的少数应用需要控制资源的直接使用 cgroup 是较好的选择，可以按用户或用户组控制系统资源。如果服务需要指出多种环境，那么 Docker 就是最好的。
	* 镜像管理: AUFS
		* 在启动docker的时候，需要指定使用的镜像？ 跟这个有关系？ 
		* 所有container都是从imag 构建的 
#### 什么是container: 
* 没有OS vir所需的mem要求


#### 先看看什么是LXC
LXC是轻量级的虚拟化，基于linux内核的一些功能 

* cgroups  具体是什么还不清楚 
为特定的进程组限定可用的资源（实际就是共享了这些resources）
* 一个有关的 chroot的 system call ？？？？     
* 具体还是不知道 LXC 是怎么实现的

#### 为了增加 container的可移动性
docker 使用了 AUFS 技术


## Motivation？ 
增加share的东西, 其实是另一种idea，和hardw/ vir 不是一个思路


## how to use it?   尝试 docker 


## 看一下什么是 KVM？ 
[相关的paper](https://www.kernel.org/doc/ols/2007/ols2007v1-pages-225-230.pdf)

## Ref
两篇文章 from Remzi
[Oracle](http://www.oracle.com/technetwork/server-storage/solaris/documentation/consolidating-apps-163572.pdf) [Docker项目](http://delivery.acm.org/10.1145/2610000/2600241/11600.html?ip=202.38.93.97&id=2600241&acc=ACTIVE%20SERVICE&key=BF85BBA5741FDC6E%2EA4F9C023AC60E700%2E4D4702B0C3E38B35%2E4D4702B0C3E38B35&CFID=638174379&CFTOKEN=12615882&__acm__=1467295192_7d83bb7117b41948a568129b237d4abf)

[百度文库的一个介绍](http://yuedu.baidu.com/ebook/d817967416fc700abb68fca1?pn=1&rf=http%3A%2F%2Fyuedu.baidu.com%2Febook%2Fd817967416fc700abb68fca1)
[百度baike的介绍](http://baike.baidu.com/item/Docker)
