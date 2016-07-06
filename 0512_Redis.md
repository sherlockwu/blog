# Redis & MongoDB 
写这篇Blog的目的是学习一下Redis（它据称是NoSQL的DB）

## 整体的感觉
应该都是NoSQL的DB，但是Redis完全在Mem中，所以可能速度更快；而MongoDB亮点在于提供复杂数据结构存储的支持
但是，还是先把SQL学完，然后，开始看一些这个MongoDB，然后Redis
## 开篇
* 存储引擎 eg BerkleyDB  Document-Oriented DB MongoDB  Key/Value Redis
* Redis 易学， 并且为一些特殊问题提供了极好的解决方案
* NoSQL 检索key从而检索数据 
* Redis 数据修改在 mem中，一定时间点disk I/O 进行备份

## 学习
可以先看Redis入门，然后再学一学怎么用
### intro
五种数据结构 & 一些数据model 
### Basics
1. Redis中database就简单用数字  select x 使用database
2. key/ values存储: key 标志, values 真正的data(只以byte关心)
	`set key value` 	`get key` 
3. querying: key 是关键
4. Mem and Persistence 在一定时间或者一定数量key变化之后，会备份到disk/ 但是设计者也认为in-mem是一种有效的方法

### Data Structures
介绍五中不同的data structure, 为什么重要？ 

* 针对不同的str， 有不同的command
* `flushdb` 删除db 
* structure
	* String 
	```
	set t_1 "SherlockWu"
	get t_1 
	```
	还有一些针对string value操作的函数: `strlen t_1(长度)` `getrange t_1 0 7(截一段出来)` `APPEND t_1 " is an undergraduate" (在后面添加)`
	如果存的是integer 可以`inc` `incrby` 操作等
	有一些bit操作没太看懂？？？  	
	* Hash 
	value 是 一系列的 (field, value) 
	设定： `hset/hmset key field value`
	查询: `hget/hmget key field`
	对hash中的field操作 `hkeys key(查询key中有哪些field)` `hdel key field (删除这个key的某个field)` 
	* List （一个key对应一个list, list也可以用index访问）
	有`lpush` `lrange` `ltrim` 等命令,注意时间衡量, eg. O(N) 
	[很详细的一个参考](http://www.cnblogs.com/stephen-liu74/archive/2012/03/16/2351859.html) [一个中文的参考](https://redis.readthedocs.io/en/2.4/list.html)
	* Set
	`sadd friend kanwu sherlock` 新建一个set的key-value对; 
	`sismember friend kanwu` 判断是否在这个set中
	`sinter friend_1 friend_2` 两个set 求交
	`sinterstore co_friend friend_1 friend_2` 交之后存起来
	* Sorted Set 
	有score的set, 支持按照score来sort. 整个set
	`zadd score_kanwu 100 pyshics 150 math 122 english` 新建一个sorted set(score, member)
	`zcount score_kanwu 100 130` count score在min/max 之间的members
	`zrevrank score_kanwu math` 取排名(从大到小 0-...)

### 使用data structure
* 每个command 有O 的时间衡量
* multi key query(想使用多个key访问到同一个value，redis not intend to support, 但我们可以使用hash来实现)  参考小红书
*** 告一段落, 高级的function没有看***




## OS X 下安装 Redis
[参考1](http://yijiebuyi.com/blog/d8ab4b444c16f42cefe30df738a42518.html) [参考2](http://my.oschina.net/jackieyeah/blog/524583)
1. 下载make
```
tar xzf redis-2.4.6.tar.gz
cd redis-2.4.6
make
```
应该也可以`brew install redis` 没有尝试
2. 开启server `./src/redis-server`
3. cli连接到server `./src/redis-cli`
4. redis 应该也有很多支持别的pl 使用的api driver 



## Reference
[Redis 的在线教程](http://try.redis.io)
[似乎这个Redis教程很完备](http://www.cnblogs.com/stephen-liu74/archive/2012/04/16/2370212.html)
[Github 上一本Redis的入门书籍](https://github.com/sherlockwu/the-little-redis-book/blob/master/en/redis.md)
[MongoDB.pdf]()
[Redis菜鸟教程](http://www.runoob.com/redis/redis-tutorial.html)
[我感觉这个说的挺清晰](http://www.cnblogs.com/hanwenhuazuibang/p/3652238.html)