# Python_3 高级特性
更高端，简洁地实现一些编程任务

## 高级特性 
* 切片
	* 取list/tuple/string中的几个元素; tuple也可以切片，但是切出来的仍然是tuple； 字符串同理
	* 格式: `XXX[起始:结束：跳步]`
	* 可以结合-k 取倒数几个元素;  然后跳步也可以是<0的 启示，结束不输默认为第一个，最后一个
	* eg ` array[::-1]` 倒着输出
	* [这个讲的挺好](http://www.cnblogs.com/buro79xxd/archive/2011/05/23/2054493.html)
* 迭代   `for .. in .. `
	* list常用, 但tuple, dict, string都可以迭代
		* eg 
		```
		L = ["sher", "holme", "Hello", "1", "2"]
		for name in L: 
        print("%d: %r" %(k, name))
        k = k+1 
		```
		* eg2 
		```
		for ch in "Sherlock"[::2]:
        print(ch)

		```
		* eg3
		```
		d_1 = {'Sherlock':1, "Holmes":2, "Watson":3}
		for people in d_1:
        	print("%r:%r" %(people,d_1[people]))
		```
		但是输出的顺序就不确定了,
		也可以以value来循环
		```
		for number in d_1.values():
        	print(number)  
		```
	* `from collections import Iterable` 然后`isinstance(xxx, Iterable)` 判断
		* eg 
		`est_1 = isinstance([1,2,3],Iterable)`
	* 实现类似 java的 按下标循环  
		* 使用 enumerate 把 list变成 index-parameter  然后循环
		* eg 
		```
		for count, name in enumerate(L):
        	print(count, name)

		```

* 列表生成式
	生成list（每个元素有固定的生成式，正规说就是有通项的数列）， 用以迭代
	* 先讲一个 range()
		`range(x,y,s)` 生成从x到y，步数为s的list（不包括y）
	* 生成式 语法 
		`L = [x * x for x in range(1, 11)]`
	* 添加if 筛选
		`L = [x * x for x in range(1, 11) if x % 2 == 0]`
	* 使用双迭代变量的循环
		`L_1 = [l*j for l in range(1,3) for j in range(3,1,-1)]`
		注意l应该是主变量，j为副变量，这样生成list的
	* 还有特殊的：
		```
		d_1 = {'Sherlock':1, "Holmes":2, "Watson":3}
		L_2 = [name+":"+ str(count) for name, count in d_1.items()]f
		```
		python 3 直接用items 不用iteritems

* 生成器
	接着列表生成式，不生成整个list，而是边循环边推算下一个循环项
	* try: 将list生成器的[] 改成() 就生成了一个generator 
		* 它保存算法,然后在循环中每次用next(g) 来取下一个
		* 但是for 循环中可省略next(g) eg.
			```
			g = (x*x for x in range(10))
			for k in g: 
				print(k)
			```
	* 最好用的是，generator可以使用任意define的函数来定义下一项如何生成
		* 原理，这个函数中一定要有 yield x 来标示next 是x, 然后只要能不停的yield, generator 就会正常工作
			eg. 
			```
			def odd():
    			print('step 1')
  	  			yield 1
    			print('step 2')
    			yield(3)
    		for k in odd()
    		```
		* 一个特殊的: `try except as ...`  这里没有记录  [参考liaoxuefeng](http://www.liaoxuefeng.com/wiki/0014316089557264a6b348958f449949df42a6d3a2e542c000/0014317799226173f45ce40636141b6abc8424e12b5fb27000)
		最后一个循环抛出 `StopIteration`



* 迭代器
	有点总结的意思 Iterable

## 函数式编程
Python 不是纯函数语言（抽象层次极高），但是有特点： 允许函数作为传参，允许返回函数

* 高阶函数
	* 函数可以赋给任一变量
	* 函数名是指向函数的变量
	* 函数可以做为参传过去, eg: 
	```
	def add(x_1, x_2, f):
		print(f(x_1)+ f(x_2))
	add(-5, 5, abs) 
	```
	* map/reduce 
		* Python 提供的两个搞抽象度的函数
		* 解释： 
			* map(f,Iterable) f作用在Iterable中的每个元素，然后得到一个Iterable, 注意list(转换一下)
			* reduce(f, [x1, x2, x3, x4]) = f(f(f(x1, x2), x3), x4)
		* 使用实例：
			**str2int 函数**  
			```
			def char2num(x_char):
				return {'0':0, '1':1, '2':2, '3':3, '4':4, '5':5, '6':6, '7':7, '8':8, '9':9}[x_char]
	 
			def list2num(x, y):
				return x*10 + y

			str_tmp = "123456"
			print(reduce(list2num, map(char2num, str_tmp)))
			```
			注意上文这个使用set的特殊技巧，很好用 
	* 使用lambda 表达式 临时定义函数: [参考知乎](https://www.zhihu.com/question/20125256)
	* filter
		和map(f, l) 类似，将f作用在l的每个元素上，然后根据返回的是true/ false 过滤元素(true 留下) -- 起到筛选的作用 
		* 一个例子： 写一个generator，每次返回next prime
			* def的函数返回值可以是一个 func， 所以可以用来做filter的第一项，每次用不同的函数
			* 尝试: 使用不断使用第一个数mod 的方法，不断得到 next(prime) 
			```
				def prime_g(): 
					Maxl = 100000
					prime_l = range(2, Maxl)
					# next prime 
					while True: 
						num = prime_l[0] 
						yield num
						prime_l = filter(lambda x: x % num > 0, prime_l)
				
				# test 
				count = 1
				prime_s = prime_g()
				while count < 1000: 
					num = next(prime_s)
					print(num)  
					count += 1 
			```
	* sorted 
		Python 提供的高级的排序算法提供两个参数
		1. eg. `sorted([9,1,3,4])`
		2. `key= abs`/ `key=str.lower` 先作用到list每个元素，再排序 `sorted([20, -15,  10, 50], key=abs) [10, -15, 20, 50]`   这个函数也可以是自己写的
			`L2 = sorted(L, key=by_name)` 更或者使用lambda函数  是好用的！
		3. `reverse = True` 反向排序选项

* 返回函数
	“闭包” 的程序结构 [参考](http://www.liaoxuefeng.com/wiki/0014316089557264a6b348958f449949df42a6d3a2e542c000/001431835236741e42daf5af6514f1a8917b8aaadff31bf000)
	只知道一个，一个func可以返回一个func, 并且可以使用func的参数或局部变量
* 匿名函数   讲的就是lambda 函数 lambda 输入: 返回值
* 装饰器 
	动态增加一个func的功能
* 偏函数

## 模块
一个 .py 就是 一个module  还有package组织的方法（解决不同module下的同名函数） 将冲突的module组织进不同的package里
a packege 将 b module 改名为 a.b, 每个包底下有`__init__.py` 文件（标志这个dir是一个package）  

* 使用模块
	* 编写一个模块
	* 导入一个模块 `import sys`  之后sys代表这个模块， 使用sys调用这个模块的各个功能. eg. sys.argv 存了一个list，表示命令行的所有参数
		* 另eg. 
		```
		import learn_2
		learn_2.greeting(name_1)
		```
	* `if __name__=='__main__': test()`  当直接命令行执行这个模块时，__name__为__main__ ， 如果是被调用则不成立， 此特性用来多执行一些测试代码
		***竟然发现还是要使用 python3 编译为好***
	* private 变量名定义 `_xxx`
	eg.
	```
	def greeting(name_1):
	temp_len = len(name_1)
	if temp_len<=5: 
		_greet_1(name_1)
	else: 
		_greet_2(name_1) 
	```
* 安装第三方模块
	* 使用包管理器pip
	* eg. `pip install pillow`


## Reference 
[廖雪峰的Blog](http://www.liaoxuefeng.com/wiki/0014316089557264a6b348958f449949df42a6d3a2e542c000/0014317568446245b3e1c8837414168bcd2d485e553779e000)