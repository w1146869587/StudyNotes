# CentOS安装CMAKE 

1、下载cmake

yum install -y gcc gcc-c++ openssl-devel

2、解压

tar -xf  

3、报错

Could NOT find OpenSSL, try to set the path to OpenSSL root folder in the system variable OPENSSL_ROOT_DIR (missing: OPENSSL_CRYPTO_LIBRARY OPENSSL_INCLUDE_DIR) 
CMake Error at Utilities/cmcurl/CMakeLists.txt:454 (message):
  Could not find OpenSSL.  Install an OpenSSL development package or
  configure CMake with -DCMAKE_USE_OPENSSL=OFF to build without OpenSSL.

-- Configuring incomplete, errors occurred!
See also "/root/cmake-3.17.0-rc2/CMakeFiles/CMakeOutput.log".

See also "/root/cmake-3.17.0-rc2/CMakeFiles/CMakeError.log".
---------------------------------------------

Error when bootstrapping CMake:

————————————————
版权声明：本文为CSDN博主「游离态De猫」的原创文章，遵循CC 4.0 BY-SA版权协议，转载请附上原文出处链接及本声明。

yum install openssl-devel -y



Linux cmake安装，配置以及测试

编号1993 2015-05-19 14:43:12  14791  收藏
展开
安装

cmake-3.2.2.tar.gz

解压：tar zxvf cmake-3.2.2.tar.gz 得到 cmake-3.2.2

进入cmake-3.2.2：cd cmake-3.2.2

./bootstrap --prefix=/home/zj/cmake_install

#prefix后跟安装目录

make

make install





kylin:

sudo apt-get install openssl

sudo apt-get install libssl-dev



## apt-get执行原理

如果仅仅知道怎么用而不知道为什么这么用，那就违背了学习使用linux的初衷，所以我们还是需要从原理出发来看apt-get指令时怎么运行的。

### 提出问题

首先需要知道的问题是：

- 我们用apt-get下载的软件包是从哪里来的？
- 下载之前要做哪些准备工作？

### 软件从哪里来？

所有的deb包由官方统一管理，那为什么我们能定位到这些软件包呢？这里就涉及到一个软件源的概念，在/etc/apt/目录下有一个sources.list文件，我们来看一下这个文件的内容：

```
cat /etc/apt/sources.list  

deb http://security.ubuntu.com/ubuntu trusty-security main restricted
deb-src http://security.ubuntu.com/ubuntu trusty-security main restricted
deb http://security.ubuntu.com/ubuntu trusty-security universe
deb-src http://security.ubuntu.com/ubuntu trusty-security universe
deb http://security.ubuntu.com/ubuntu trusty-security multiverse
deb-src http://security.ubuntu.com/ubuntu trusty-security multiverse
deb http://extras.ubuntu.com/ubuntu trusty main
deb-src http://extras.ubuntu.com/ubuntu trusty main
deb http://us.archive.ubuntu.com/ubuntu/ trusty-proposed main restricted multiverse universe   
```

由于条目太多，这里只贴出一部分。可以看出来的是，这里都是一些资源网站，软件包资源当然就是出自这里。