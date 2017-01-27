# x86汇编

[很好的教程](http://blog.sina.com.cn/s/blog_70dd16910100r6oj.html)
cmp 就是 做差，但是不该dest而已
[各种指令的介绍](http://blog.csdn.net/bekilledlzy/article/details/1765802)

[call function 用stack传递参数](http://netclass.csu.edu.cn/NCourse/hep094/homepage/07-3-3.htm)

```
ADDRESS_OR_OFFSET(%BASE_OR_OFFSET,%INDEX,MULTIPLIER)

它所表示的地址可以这样计算出来：

FINAL ADDRESS = ADDRESS_OR_OFFSET + BASE_OR_OFFSET + MULTIPLIER * INDEX

其中ADDRESS_OR_OFFSET和MULTIPLIER必须是常数，BASE_OR_OFFSET和INDEX必须是寄存器。在有些寻址方式中会省略这4项中的某些项，相当于这些项是0。
```

push 压栈前， sp-4