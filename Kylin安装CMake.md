# Kylin安装CMake

## 1、查看openssl的版本

openssl version -a



### 问题

# [linux 安装软件出现：“E：无法定位软件包”](https://www.cnblogs.com/ch-123/p/10746202.html)

今天学习Linux安装一个软件时，一直跳出“E: 无法定位软件包”的错误，无法安装。

更新了源镜像为清华大学的源后也不行，随后在网上浏览，看到了一个解决办法：

在etc/apt/sourcrs.list 文件后面添加deb http://archive.ubuntu.com/ubuntu/ trusty main universe restricted multiverse ，然后sudo apt-get update即可



### 问题

loading initial cache file /home/wah/cmake-3.17.3/Bootstrap.cmk/InitialCacheFlags.cmake
-- Could NOT find OpenSSL, try to set the path to OpenSSL root folder in the system variable OPENSSL_ROOT_DIR (missing: OPENSSL_CRYPTO_LIBRARY OPENSSL_INCLUDE_DIR) 
CMake Error at Utilities/cmcurl/CMakeLists.txt:454 (message):
  Could not find OpenSSL.  Install an OpenSSL development package or
  configure CMake with -DCMAKE_USE_OPENSSL=OFF to build without OpenSSL.



#### 问题

Could NOT find OpenSSL, try to set the path to OpenSSL root folder in the system variable OPENSSL_

只爱写代码 2019-03-25 22:17:33  1275  收藏 2
展开
1.安装cmake
apt install cmake
1
2.安装openssl和编译依赖
apt install openssl
apt install libssl-dev



 银河麒麟的软件源

![img](https://csdnimg.cn/release/phoenix/template/new_img/reprint.png)

[ciji4412](https://me.csdn.net/ciji4412) 2019-08-16 08:00:00 ![img](https://csdnimg.cn/release/phoenix/template/new_img/articleRead.png) 7918 ![img](https://csdnimg.cn/release/phoenix/template/new_img/collect.png) 收藏 3

展开

银河麒麟官方更新了国际互联网可用的软件源，请参阅：http://archive.kylinos.cn/kylin/KYLIN-ALL/

软件源使用方法

在系统的/etc/apt/sources.list文件中，根据不同版本填入以下内容

\#4.0.2桌面版本:
deb http://archive.kylinos.cn/kylin/KYLIN-ALL 4.0.2-desktop main restricted universe multiverse

\#4.0.2-sp1桌面版本:
deb http://archive.kylinos.cn/kylin/KYLIN-ALL 4.0.2sp1-desktop main restricted universe multiverse

\#4.0.2-sp2桌面版本:
deb http://archive.kylinos.cn/kylin/KYLIN-ALL 4.0.2sp2-desktop main restricted universe multiverse

\#4.0.2服务器版本:
deb http://archive.kylinos.cn/kylin/KYLIN-ALL 4.0.2-server main restricted universe multiverse

\#4.0.2-sp1服务器版本:
deb http://archive.kylinos.cn/kylin/KYLIN-ALL 4.0.2sp1-server main restricted universe multiverse

\#4.0.2-sp2服务器版本:
deb http://archive.kylinos.cn/kylin/KYLIN-ALL 4.0.2sp2-server main restricted universe multiverse

\#4.0.2-sp2 FT2000+服务器版本:
deb http://archive.kylinos.cn/kylin/KYLIN-ALL 4.0.2sp2-server-ft2000 main restricted universe multiverse

\#4.0.2-sp3桌面版本:
deb http://archive.kylinos.cn/kylin/KYLIN-ALL 4.0.2sp3-desktop main restricted universe multiverse

转载于:https://my.oschina.net/chipo/blog/3093242



## 安装步骤

1、先按照kylin版本，设置apt-get的源

2、更新源sudo apt-get update

3、安装openssl
apt install openssl
apt install libssl-dev

4、网站下载cmake源码

./configure

gmake /make

gmake install/make install







