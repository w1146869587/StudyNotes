# ubuntu qt平台搭建openssl开发环境

![img](https://csdnimg.cn/release/blogv2/dist/pc/img/original.png)

[skytering](https://me.csdn.net/skytering) 2019-11-08 17:00:33 ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/articleReadEyes.png) 727 ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/tobarCollect.png) 收藏 3

分类专栏： [ubuntu](https://blog.csdn.net/skytering/category_9331463.html) [openssl](https://blog.csdn.net/skytering/category_9496919.html) [qt](https://blog.csdn.net/skytering/category_9496920.html) 文章标签： [openssl](https://www.csdn.net/gather_21/MtTaEg0sMTk0MDItYmxvZwO0O0OO0O0O.html) [qt](https://so.csdn.net/so/search/s.do?q=qt&t=blog&o=vip&s=&l=&f=&viparticle=) [ubuntu](https://www.csdn.net/gather_2e/MtTaEg0sNTA1ODktYmxvZwO0O0OO0O0O.html)

版权

ubuntu qt平台搭建openssl开发环境

# 1、下载解压

（这里以当前官网下载的最新版本为例，官网地址：http://www.openssl.org/source）
tar -zxvf openssl-1.1.1d.tar.gz
mv openssl-1.1.1d openssl

# 2、编译安装

cd openssl
./config --prefix=/usr/local/ssl shared zlib-dynamic enable-camellia
make depend
make
make test
sudo make install

# 3、配置

设置环境变量：
在/etc/profile的PATH中增加如下内容
PATH=/usr/local/ssl/bin:$PATH
export PATH

查看路径
which openssl

查看版本
openssl version

安装完毕

# 4、qt项目添加头文件配置

pro项目配置文件中添加：
INCLUDEPATH += /usr/local/ssl/include

# 5、qt项目添加openssl动态库配置

pro项目配置文件中添加：
LIBS += /usr/local/ssl/lib/libssl.so /usr/local/ssl/lib/libcrypto.so

# 6、添加运行库的搜索路径

在/etc/ld.so.conf.d/目录下新建ssl.conf的文件，在该文件中加入库文件所在的目录
/usr/local/ssl/lib
执行
sudo ldconfig
以更新/etc/ld.so.cache文件；