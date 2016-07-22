# RethinkDB 入门
主要是:
1. 看一下 RethinkDB 到底是个什么
2. 总体掌握以下 NoSQL
3. 会用RethinkDB 的相关东西

## NoSQL 
* 主要应该就是 牺牲 consistency 来help distribute 等
* 可以有很多的 data model: eg document-oriented 

#### document-oriented
* 每个document像一个object一样存储（类似key-value）, 但是可以查询object中的域的内容（不同于key-value）  
* db中每个 record 对应 一个 有结构的 document(每个document有自己的一些fields): 这是最不同于RDB的地方，每个record不一定有相同的一些fields
* 一般一个document会配一个 metadata，方便查询等
* **key**  
	* database 通过每个document对应的key来查询 document （这个key 可以是URL 或 path这样的东西）
	* Retrivel: 
		* (**不同于key-value的地方**)除了用key查询document, db支持用户使用特定的内容（一个field:value的对）查询document
		* db 使用metadata 分类documents  ？？？？ 这和上一个功能有没有什么关系？ 
* Updating: 
	* db 允许用户修改整个doc， 或doc的一些fields

#### key-value db

## 官方的介绍: 
* scalable 的database for building realtime apps;  
	* 直接query JSON
	* 新结构: RethinkDB 连续向developer 推送变化的query results 
	* [参考文档](https://www.rethinkdb.com/faq/)

## 安装尝试: 
* 安装rethinkdb， [参照](https://www.rethinkdb.com/docs/guide/javascript/)
* 安装 Node.js [参照](http://www.runoob.com/nodejs/nodejs-install-setup.html)
* 尝试:
	* [参照了这个Blog的操作](http://www.cnblogs.com/cocoajin/p/3678307.html)
* 几个命令: [参照](https://www.rethinkdb.com/api/python/#run)
	1. `import rethinkdb as r`
	2. `conn = r.connect('localhost', 28015)` or `conn = r.connect(db='test')`
	3.  `conn.repl()` 可以设置某个connection为默认连接， run() 不用带conn参数 
	4. `query.run(conn)` 可以省略conn, 返回一个cursor或者一个object，根据不同的query
	5. `changes` 订阅一个table的变化
	6. `insert` document 
	7. `filter` 过滤一些documents
	8. 
* 

## Ref 
1. [官方介绍](https://www.rethinkdb.com)