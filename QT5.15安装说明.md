# QT5.15安装说明 



一、Qt 发布公告（2020年5月28日）：

http://download.qt.io/official_releases/qt/5.15/5.15.0/OFFLINE_REAMDE.txt

    Due to The Qt Company offering changes, open source offline installers are not available any more since Qt 5.15. Read more about offering changes in the https://www.qt.io/blog/qt-offering-changes-2020 blog.
     
    If you need offline installers, please consider our new Qt for Small Business offering: https://www.qt.io/blog/available-now-qt-for-small-businesses。

大意是：从 Qt 5.15 开始，开源版本，无论是不是 LTS，不再提供编译后的独立安装包，只能在线安装。

如果确实需要离线安装包，则要购买 Qt for Small Business 产品。

https://www.qt.io/blog/available-now-qt-for-small-business

二、Qt 在线安装器下载网址：

http://download.qt.io/official_releases/online_installers/





今天在安装软件的时候出现了Package has no installation candidate的问题，如：

    #  apt-get install <packagename>
    Reading package lists... Done
    Building dependency tree... Done
    Package aptitude is not available, but is referred to by another package.
    This may mean that the package is missing, has been obsoleted, or
    is only available from another source
    E: Package <packagename> has no installation candidate 


解决方法如下：
# apt-get update
# apt-get upgrade
# apt-get install <packagename>

这样就可以正常使用apt-get了～