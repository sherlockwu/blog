# 读 OS: three easy pieces

## Preface: 
* 编程任务: 我应该以xv6 编程 为主。
* 主要关心:	
	* virtulization 
	* concurrency 
	* persistance

## Intro to OS 
* OS 的主要作用: 方便program执行， 和hardware交互， 共享resource等 (核心方法是virtualize resources 然后统一API 给 APP， 方便他们使用)

## 关于virtulization的两个例子
1. CPU 的virtualization
	1. main 的argc, argv  
	2. spin 自旋锁:
		1. 解决多用户对共享资源的占有（同“互斥锁”）  但是互斥锁，如果一个用户无法拥有就休眠，but spin， 不停循环查看自旋锁是否被释放了
		2. 适用于用户对 资源占有时间 很短的 情形； 适用于SMP 的情形
	3. 得出的结论就是: 实际上一个 porcess 只face virtualized cpu
	4. 一个核心的问题就是 OS 作为 resource manager 应follow哪个policy去 把 不同的process放上去！
2. mem 的virtualization

## Ref
1. [书的网址](http://pages.cs.wisc.edu/~remzi/Classes/537/Spring2016/)