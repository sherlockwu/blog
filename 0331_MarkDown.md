# Markdown的语法&在SublimeText中的使用

## Abstract 
1. 介绍markdown的基本语法
2. 如何在sublime text（我就是喜欢用它）中书写，预览




## Markdown 书写
#### 标题如何书写
n*#

#### 列表 Bulletin
就是使用一般的 *(对应点) 或 1/2/3，例如： 

> *  1st Type 
>
> 1. 另外一种
> 2. 都需要和正文之间隔space


#### 链接&图片
	 1. [文字](链接地址)  例如： 
> 	[吴衎的科大主页](http://home.ustc.edu.cn/~wukanust)
>	注意网址之前一定要加(http://)

	2. "![]（）" 例如：
>	![](http://home.ustc.edu.cn/~wukanust/images/self_1.jpg)

#### 引用 
1. 使用> 内容就好
2. 引用也是可以 嵌套的（多个> ）

> hello
>> not bad 
> bye  

3. 引用中也能有标题，例如:
> hello
>> #### this is a quota 

#### 粗体&斜体
1. 用* 两侧包围： 斜体
2. 用** 两侧包围： 加粗尝试： 

> *Hello*, **Kan Wu** 


#### 表格
1. |标题     | 理论上都是 | 居中的   | 
2. | ---顶左- |:---居中--:| --顶右-:|
3. |1       | 2		 | 3       |   
4. |4       | 5         | 6       |

|标题     | 理论上都是 | 居中的   | 
| ---顶左- |:---居中--:| --顶右-:|
|1       | 2		 | 3       |   
|4       | 5         | 6       |

注意格式: |空格---冒号|

#### 直接使用Latex 
* 两种:

> 1. ![][1]
> [1]:http://latex.codecogs.com/gif.latex?\sum\(n_{j}\)+1
> 2. 或者：(直接把Latex网址放在图片链接中)
> ![](http://latex.codecogs.com/gif.latex?\prod\(n_{j}\)+1)
> 3. [一个很好的Latex公式网站](http://mohu.org/info/symbols/symbols.htm)


## 结合Sublime Text 2 使用
> 1. package control: (cmmd+shift+p) 
> 2. package install: Markdown Preview
> 3. 然后每次： 使用markdown 在 browser 中打开即可 (Github 和 Markdown 稍微有一点区别)


## PROBLEMS: 

1. 所以怎么应用代码这样？ 使用 tab 实际上是相当于quota，例如： 

this is with out `tab` 
	
	this is with tab
		hello (two tab)

> this is with >(quota)
>> more one layer
> * hello 
	my guy hello
	

## What's New? 
1. 使用两个`  可以加深字体    
`eg`

## Summary
**现在我需要记得的：** 
>	1. 格式： 多用> 来分层 或者直接打字, Tab 有点像单独的一句话，也可以用
>	2. 不同类型的东西之间还是要多一个换行
> 	3. 标题： n*#   两个标题还是差两个#比较能分得开
>	4. 链接，图片，多用用
>	5. 表格用的机会可能不多，但是可以尝试多用
>	6. 直接用 Latex 还是可以的

## Reference
[1 一个简洁的介绍](http://www.jianshu.com/p/q81RER) 
[2 一个结合html(MarkDown与html互相转换)的介绍](http://wowubuntu.com/markdown/)
[3 CSDN的功能说明](http://write.blog.csdn.net/mdeditor)
