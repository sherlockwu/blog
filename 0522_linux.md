# Linux 配置

## 软件源
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


### rpm 包软件管理程序
wget 很好用  wget+ 地址
[使用参考](http://blog.csdn.net/neohuo/article/details/600339)

### shutdown 指令
`shutdown -hr time`
h halt  r reboot time 表示多久  now 现在
[鸟叔的](http://linux.vbird.org/linux_basic/0160startlinux.php)

## Reference 
[一个PPT](https://lug.ustc.edu.cn/OpenCourse/Lesson8/lesson8.pdf)