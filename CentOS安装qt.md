# 安装 opengl（dbus编译依赖于opengl）

yum install -y mesa*

yum install -y freeglut*

yum install -y \*GLEW\*

# 运行qt 报错

“cannot find -lGL”

可以使用`locate libGL`命令或`find /usr -name libGL*`命令查找，然后使用`ln -s`创建链接。请看下面的演示：

\#查找 libGL 所在位置
[root@localhost ~]# locate libGL
/usr/lib64/libGL.so
/usr/lib64/libGL.so.1
/usr/lib64/libGL.so.1.2.0
/usr/share/doc/mesa-libGL-9.2.5
/usr/share/doc/mesa-libGL-9.2.5/COPYING

\#创建链接
[root@localhost ~]# ln -s /usr/lib64/libGL.so.1 /usr/lib/libGL.so

#  undefined sysmbol:FT_Get_Font_Format

yum install -y freetype-devel







## Ubuntu安装QT5

技术标签： [QT](http://www.pianshen.com/tag/QT/) [QT5](http://www.pianshen.com/tag/QT5/) [QT安装](http://www.pianshen.com/tag/QT安装/) [Ubuntu](http://www.pianshen.com/tag/Ubuntu/) [qtcreator](http://www.pianshen.com/tag/qtcreator/)

[PropellerAds](https://propellerads.com/?utm_medium=widget&utm_source=propellerads&utm_campaign=branding)

Recommended



![img](http://3x2.myfastcdn.com/contents/s/e7/da/26/0383f97b5b608a0665de1018b5/0613050239091.jpeg?width=492)

如何开始过上奢华的生活，再也不用工作



![img](http://3x2.myfastcdn.com/contents/s/94/44/25/771b306dca942ef0fe971e2dc4/01384679056179.jpeg?width=492)

您認識這位女孩嗎？她就住在離您3個街區的地方



![img](http://3x2.myfastcdn.com/contents/s/e8/5d/e1/9674ada1b06b7f6e04c3a67906/01151910052865.jpeg?width=492)

1個月輕鬆獲得比基尼身材

# 前言

最近打算学一下QT应用程序开发，所以打算装一个QT桌面环境QtCreator，捣鼓了一阵，把电脑弄坏重装系统之后，终于安装好了，这里分享一下安装的过程

# 1. QT5安装

环境

```
Ubuntu14.04
QT5.12.3
12
```

首先去[QT安装包](https://download.qt.io/archive/qt/)下载安装包，我这里选择的是目前最新的QT5.12.3
![QT安装包](http://www.pianshen.com/images/314/17c935ec964c639aaabaf84ab761cb6a.png)
下载好之后赋予可执行权限

```c
chmod +x qt-opensource-linux-x64-5.12.3.run
1
```

然后执行安装命令

```c
sudo ./qt-opensource-linux-x64-5.12.3.run
1
```

然后一直点下一步或者跳过就好了，安装路径我也是默认的
![QT安装路径](http://www.pianshen.com/images/838/e08961edead32ea5e8d1fa220a7a2dbe.png)
等待安装完成

# 2. 路径配置

安装完成之后，需要修改default.conf，执行

```c
sudo vim /usr/lib/x86_64-linux-gnu/qt-default/qtchooser/default.conf
1
```

将第一行改为自己安装路径下的bin目录的路径，第二行改为Qt5.12.3目录的路径，下面是我的配置

```c
/opt/Qt5.12.3/5.12.3/gcc_64/bin
/opt/Qt5.12.3/
12
```

# 3. 运行问题

## 3.1 FT_Get_Font_Format

运行qtcreator，然后报错undefined symbol: FT_Get_Font_Format

```c
anruliu@anruliu:/opt/Qt5.12.3/Tools/QtCreator/bin$ ./qtcreator
./qtcreator: symbol lookup error: /opt/Qt5.12.3/Tools/QtCreator/lib/Qt/plugins/platforms/../../lib/libQt5XcbQpa.so.5: undefined symbol: FT_Get_Font_Format
12
```

需要下载安装[freetype-2.10.0](https://download.savannah.gnu.org/releases/freetype/)，解压之后执行

```c
cd freetype-2.10.0
./configure --prefix=/opt/Qt5.12.3/Tools/QtCreator/lib/Qt/
make
cd ./objs/.libs
sudo cp libfreetype.so /opt/Qt5.12.3/Tools/QtCreator/lib/Qt/lib
sudo cp libfreetype.so.6 /opt/Qt5.12.3/Tools/QtCreator/lib/Qt/lib
sudo cp libfreetype.so.6.17.0 /opt/Qt5.12.3/Tools/QtCreator/lib/Qt/lib
1234567
```

其中/opt/Qt5.12.3/就是安装QT的目录

## 3.2 LIBDBUS_1_3 not defined

再次运行qtcreator，然后报错version LIBDBUS_1_3 not defined

```c
anruliu@anruliu:/opt/Qt5.12.3/Tools/QtCreator/bin$ ./qtcreator
./qtcreator: relocation error: /opt/Qt5.12.3/Tools/QtCreator/lib/Qt/plugins/platforms/../../lib/libQt5DBus.so.5: symbol dbus_message_get_allow_interactive_authorization, version LIBDBUS_1_3 not defined in file libdbus-1.so.3 with link time reference
12
```

需要下载安装[dbus-1.13.10](https://dbus.freedesktop.org/releases/dbus/)，解压之后执行

```c
cd dbus-1.13.10
./configure --prefix=/opt/Qt5.12.3/Tools/QtCreator/lib/Qt/
make
cd ./dbus/.libs
sudo cp libdbus-1.so /opt/Qt5.12.3/Tools/QtCreator/lib/Qt/lib
sudo cp libdbus-1.so.3 /opt/Qt5.12.3/Tools/QtCreator/lib/Qt/lib
sudo cp libdbus-1.so.3.26.0 /opt/Qt5.12.3/Tools/QtCreator/lib/Qt/lib
1234567
```

其中/opt/Qt5.12.3/就是安装QT的目录
把缺失的库直接拷贝到qtcreator的lib的路径下，可以让qtcreator找到它自己需要依赖的库，不会对系统本身造成影响，不然可能会导致桌面起不来，然后得重装系统

所有问题解决后，运行qtcreator，就可以看到界面，可以尽情的开发了
![qtcreator运行效果](http://www.pianshen.com/images/572/8e84bf392fa0bc02739f72f9d67bfcfc.png)

# 4. 编译应用问题

在示例中选择一个demo进行编译，比如我选的是shadow-map-qml，在构建设置配置好后，点击运行，发现还有一些错误

## 4.1 GL/gl.h: No such file or directory

```c
/opt/Qt5.12.3/5.12.3/gcc_64/include/QtGui/qopengl.h:144: error: GL/gl.h: No such file or directory
1
```

需要安装gl的库

```c
sudo apt-get install libgl1-mesa-dev
1
```

## 4.2 LIBDBUS_1_3 not defined

```c
relocation error: /opt/Qt5.12.3/5.12.3/gcc_64/lib/libQt5DBus.so.5: symbol dbus_message_get_allow_interactive_authorization, version LIBDBUS_1_3 not defined in file libdbus-1.so.3 with link time reference
1
```

这个和运行qtcreator的错误一样，需要我们指定libdbus的目录，在项目–>构建设置–>构建环境添加环境变量LD_LIBRARY_PATH为/opt/Qt5.12.3/Tools/QtCreator/lib/Qt/lib，如下图所示
![构建设置](http://www.pianshen.com/images/663/ea568f8bdd505e7006703ddf3626bca7.png)
改好之后，重新运行，就可以看到应用运行效果了！！！
![QT DEMO](http://www.pianshen.com/images/6/54275221c88abb0b554fd26f764d5e26.png)

版权声明：本文为博主原创文章，遵循[ CC 4.0 BY-SA ](https://creativecommons.org/licenses/by-sa/4.0/)版权协议，转载请附上原文出处链接和本声明。



http://www.pianshen.com/article/3003418461/





## LD_LIBRARY_PATH
/home/wah/Qt5.13.2/Tools/QtCreator/lib/Qt/lib



export PATH="/home/wah/Qt5.13.2/5.13.2/gcc_64/bin:$PATH"