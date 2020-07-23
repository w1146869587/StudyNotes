# Gyp安装

一、安装Python

要使用Python2.x,，Python3.x会报错

二、下载

git clone https://chromium.googlesource.com/external/gyp

三、安装

1. cd gyp
2. python setup.py install

# Breakpad安装

一、拷贝gyp文件夹

拷贝gyp文件夹到breakpad\src\tools文件夹下

二、生成sln解决方案

进入刚刚拷贝的gyp目录，然后执行： 
gyp.bat –no-circular-check “../../client/windows/breakpad_client.gyp”