# Mac 下 MySQL安装
本Blog将记录在Mac下安装MySQL的过程

## 安装
* 下载
[MySQL官方下载地址](http://dev.mysql.com/downloads/mysql/)
	下载下来的应该是没有GUI的纯粹的一个DBMS（虽然应该也是够用了），还是用了Navicat 进行了connect之后再进行管理

* 安装 （本次安装的有些诡异，但是始终还是能够通过Navicat进行一些操作学习）
	1. 正常安装 
	2. 无法建立连接（must change password）

		1. 为了方便执行一些命令eg.`mysql`, 首先就是需要改一下环境路径:
		```
		$ echo $PATH %看一下
		$ PATH=/usr/local/mysql/bin/:$PATH
		```
		2. 然后需要设置一下root账户的密码:

			* 安全模式进入MySQL: `$sudo mysqld_safe --skip-grant-tables`
			* 新终端中进入MySQL: `$mysql -u root`
			* 修改密码: `$ update mysql.user set password=password('123456') where user='root'`

	3. 再次尝试登陆: `$ mysql -h localhost -u root` 输入密码成功（-h 表示连接的host, -u表示连接的用户）

* 使用
让Navicat 连接localhost 的MySQL, 然后就能GUI下新建表，Query操作，看结果等了

重启？？？？
## 再次登录出错
* 无法连接
```
$mysql -h localhost -u root -p
Enter password: 
ERROR 1045 (28000): Access denied for user 'root'@'localhost' (using password: YES)
```
 * 直接使用SQL command line 吧
 `show databases`
 `use xxxdatabase`
 开始操作

## 卸载MySQL 
[按步骤](http://www.cnblogs.com/yjmyzz/p/4558389.html)

## Reference
1. [简书的Blog](http://www.jianshu.com/p/fb695223d1a9)
2. [官方的介绍](http://dev.mysql.com/doc/refman/5.7/en/connecting-disconnecting.html)
3. [修改路径设置](https://site.douban.com/129642/widget/notes/5513129/note/382967975/)
4. [修改root密码进入](http://jacob110.github.io/2015/10/13/mac-os-install-mysql5-7/)