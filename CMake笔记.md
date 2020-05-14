# CMake笔记

# 什么是CMake 

> All problems in computer science can be solved by another level of indirection.
>
> **David Wheeler**



一些使用 CMake 作为项目架构系统的知名开源项目有 [VTK](http://www.vtk.org/)、[ITK](http://www.itk.org/)、[KDE](http://kde.org/)、[OpenCV](http://www.opencv.org.cn/opencvdoc/2.3.2/html/modules/core/doc/intro.html)、[OSG](http://www.openscenegraph.org/) 等 [[1\]](https://www.hahack.com/codes/cmake/#fn1)。



CMakeLists.txt 的语法比较简单，<u>由命令、注释和空格</u>组成，其中命令是不区分大小写的。符号 `#` 后面的内容被认为是注释。命令由命令名称、小括号和参数组成，参数之间使用空格进行间隔。

# 命令

## 1、cmake_minimum_required

指定运行此配置文件所需的CMake的最低版本;













