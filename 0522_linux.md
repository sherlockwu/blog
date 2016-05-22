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


## Reference 
[一个PPT](https://lug.ustc.edu.cn/OpenCourse/Lesson8/lesson8.pdf)