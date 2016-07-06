# Python 练习
本Blog尝试记录2W连续的Python练手， 但是实际上还是有很多的知识点还没有学习到的 
要注意项目往前make progress，但是也要注意充分学习一些东西

**看一点，尝试三题**

### 图片加水印
将你的 QQ 头像（或者微博头像）右上角加上红色的数字，类似于微信未读信息数量那种提示效果。 类似于图中效果

* 应该是两个图片合成？ 
	需要模块，打开图片  
	竟然还能图像处理！！！！ 这么强大! 
	还能绘制plots 还能根据在图像上点击交互！！！
	[太强大了](http://www.ituring.com.cn/tupubarticle/2024) 	[这个也很强大](http://oucmsc.blog.163.com/blog/static/126340328201293045017183/)
	PIL 还有 OpenCV？ 	[最后一个](http://oucmsc.blog.163.com/blog/static/126340328201293045017183/)
* 其实是用了 ImageDraw 可以在图片上draw	
* `import Image` 基础
	* ImageDraw 这个类  应该描述的是 绘画这个操作，有操作文件，操作设定等
* 无PIL module   
先得 install pip  `sudo easy_install pip`
然后装PIL `sudo pip install image` 安装pillow(改进版)   不行？
	* 尝试另一个： 
	`brew install libtiff libjpeg webp little-cms2`
	`sudo brew install Pillow`
	成功了！！！！ 但是为什么一定要 `python 1.py` 才可以！ 
	* 尝试安装了一个 xcode 的开发者工具

* 然后使用 ImageDraw
[参考](http://liam0205.me/2015/05/05/pil-tutorial-imagedraw-and-imagefont/)
注意，坐标(0,0) 为左上角

* 总结
	综合使用Image类和ImageDraw类, ImageDraw(类)有这个方法：
	`text(position, string, options)` options 可以是`fill=(R,G,B)` 设定颜色
	或者ImageFont 设定 font 
	```
		fontsize = min(x_bond, y_bond) // 11
		font_1 = ImageFont.truetype("/Library/Fonts/Tahoma.ttf", fontsize)
	
	```
	[代码参见GitHub](https://github.com/sherlockwu/python_coding/tree/master/python_practice/p_1)

*注意：
千万别乱加 tab

### 生成激活码 
设计生成 10位的任意英文字符或数字的激活码， 要保证200个，还不一样

* 用random.choice(定义域) `import random` 	[参考](http://blog.csdn.net/pipisorry/article/details/39086463) 
	* 有一个很好的设定定义域的方法： `string.ascii_uppercase + string.digits`

* 还要写向文件：	[参考](http://www.cnblogs.com/feeland/p/4477535.html)
	打开之后一定要关闭
	```
	filename = "./output.txt"
	f = open(filename, "w")
	f.write(''.join(sequence_1)+'\n' ) 
	f.close()

	```

* 一定要写编码 
	`# -*- coding: utf-8 -*-` [参考](http://www.crifan.com/python_head_meaning_for_usr_bin_python_coding_utf-8/)
* 注意：Bool 是 True/False 不是true/false  
* 将list转化成string [参考](http://piziyin.blog.51cto.com/2391349/568426)
* [Code on Github](https://github.com/sherlockwu/python_coding/tree/master/python_practice/p_2)

### 将激活码写入MySQL数据库
* [链接数据库  这个说的很好](http://www.cnblogs.com/fnng/p/3565912.html)
* [一个纠错](http://www.cnblogs.com/ifantastic/archive/2013/04/13/3017677.html)
* Mysql-python 驱动: 是一个package   
	* 下载安装包  然后 `python setup.py install`   然后修改一个path的BUG （按纠错） 
	* pip  没有尝试
* 使用MySQLdb module中的方法
	* connect 得到一个db 实例 
	* 创建游标实例
	* 通过游标实例进行 db 操作
	* db 实例提交变化/ 关闭数据库连接
* 插入string遇到了问题  调了很长时间发现一个可行的方案： `cur.execute("insert code values('%s')" %(string_1))` [参考](http://blog.csdn.net/shellshine/article/details/8207448)
* 代码实例
```
conn = MySQLdb.connect(host='localhost', port=3306, user='root', passwd='123', db='test') 
## cursor 
cur = conn.cursor() 
## create table 
cur.execute("drop table code")
cur.execute("create table code(num_1 varchar(11))") 

cur.close()
conn.commit()
conn.close()
```

### 将激活码写入 Redis 非关系数据库
* 安装pyredis  `easy_install redis` 
* 存储方式， db 0 中 `code_x` 为 key, 相应的码为value
	* integer 转string str(number)  [参考](http://blog.csdn.net/shanliangliuxing/article/details/7920400) 
	* 代码实例:
	```
	import redis


	r = redis.Redis(host="localhost", port=6379, db=0)
	r.set(string_2, string_1)
	```
	很简单的完成任务
	

### 统计文件中的单词  

## Reference 
[知乎的回答](https://www.zhihu.com/question/29372574)
[有个github练手的项目](https://github.com/sherlockwu/show-me-the-code)