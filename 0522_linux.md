# Linux 配置

### 软件源
apt yum 都是包管理器  前端
后端是 dpkg/ rpm   apt 构建与 dpkg之上, yum 以rpm为后端

rpm 提供了管理包的功能，yum则使用rpm自动帮我们安装依赖的包等


### 添加源
* `sudo vi /etc/apt/sources.list`
* 添加两个源
deb http://mirrors.ustc.edu.cn/ubuntu/ trusty main
deb-src http://mirrors.ustc.edu.cn/ubuntu trusty main restricted
* `sudo apt-get update`

### 安装VirtualBox
1. 查看 linux 版本号  `ls /etc/*issue*` 查看
2. 添加源
3. 添加 apt key 
4. dkms 
安装纯命令行的 virtualbox失败

在 OSX 安装很简单
virtualbox 可以开启 shared clipboard 复制，粘贴

调节virtual box linux 的分辨率 有一个很好的教程 [sina blog](http://blog.sina.com.cn/s/blog_489988100102ux6e.html)

### 安装 zsh
参照? 
目前不能自动打开，打开还是正常的shell

### rpm 包软件管理程序
wget 很好用  wget+ 地址
[使用参考](http://blog.csdn.net/neohuo/article/details/600339)

### shutdown 指令
`shutdown -hr time`
h halt  r reboot time 表示多久  now 现在
[鸟叔的](http://linux.vbird.org/linux_basic/0160startlinux.php)

## 一些积累
## 以前积累的
Q 1     : 无法vim 编辑根目录下的文件，除非sudo
        chmod 777 thisfile

Q 2     ：如何搜索
        grep '..*' -r .
        如果没有省略就不用单引号，不要弄错

        不区分大小写 ： -i：

Q 3     : 搜索文件
        find ./ -name '名字'
Q 4     : 安装Latex & ST
        http://www.readern.com/sublime-text-latex-chinese-under-mac.html

Q 5     : 常用的网络诊断
        ping tracerout

Q 6     : unmount disk
        diskutil unmount
        diskutil mount if=拖进来 of=/dev/disk?

Q 7     : 搭建子网
        修改 sudo gedit /etc/network/interfaces

Q 8     : mv 使用
        mv file1 file2      1改名为2
        mv file1 file2 dir  移动file1 file2 到dir

Q 9     : chmod 使用
        chmod 77 file   修改为都可以

Q10     : grep
        grep '...' ./ss  找出 ss中包含某字符串的那几行

Q11     : tar
        tar zxvf 文件    来解压

Q12     : 如何看当前路径
        pwd 

Q13     : 如何打开html的东西
        open （相当于双击这个文件）

Q14     : 如何使用Ctags
        安装ctags -> `ctags -R` 即可

## Reference 
[一个PPT](https://lug.ustc.edu.cn/OpenCourse/Lesson8/lesson8.pdf)

