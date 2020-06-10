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

### eg1:cmake_minimum_required (VERSION 2.8)

## 2、project

项目的名称

### eg1:project(demo) 

#项目名称为demo

## 3、add_executable

编译为可执行文件

### eg1:add_executable(Demo main.cc)

将main.cc编译为Demo.exe或Demo可执行文件

## 4、add_library

编译为库

### eg1:add_library ( base64 STATIC  ${src} )

编译为静态库

### eg2:add_library ( base64 SHARED  ${src})

编译为动态库

## 5、aux_source_directory

该命令会查找指定目录下的所有源文件，然后将结果存进指定变量名

aux_source_directory(<dir> <variable>)

### eg1:aux_source_directory(. DIR_SRCS)

#查找当前目录下的所有源文件,并将名称保存到 DIR_SRCS 变量

## 6、add_subdirectory

指明本项目包含一个子目录

### eg1:add_subdirectory(math)

指明本项目包含一个子目录 math，这样 math 目录下的 CMakeLists.txt 文件和源代码也会被处理

## 7、target_link_libraries

指明该项目需要链接库

### eg1:target_link_libraries(Demo MathFunctions)

使用命令 `target_link_libraries` 指明Demo项目 需要连接一个名为 MathFunctions 的链接库 。

## 8、option

让你可以根据选项值进行条件编译

option(<option_variable> "help string describing option"   [initial value])

option 提供选项让用户选择是 ON 或者 OFF ，如果没有提供初始化值，使用OFF。
也就是说默认的值是OFF

>
> 但是请注意：这个option命令和你本地是否存在编译缓存的关系很大。
> 所以，如果你有关于 option 的改变，那么请你务必清理 CMakeCache.txt 和 CMakeFiles 文件夹。
> 还有，请使用标准的 [initial value] 值 ON 或者 OFF。
> 

可以在命令行通过以下的方式设置选项
比如想打开 FOO_ENABLE 选项 -DFOO_ENABLE=ON

## 9、configure_file

configure_file 的作用是让普通文件也能使用CMake中的变量。
也就是说代码文件中可以使用CMake中的变量。

configure_file(<input>  <output>
                    [COPYONLY] [ESCAPE_QUOTES] [@ONLY]
                    [NEWLINE_STYLE [UNIX|DOS|WIN32|LF|CRLF] ])
输入文件中的
#cmakedefine VAR ...
将被替换为
#define VAR ...

### eg:
Consider a source tree containing a <u>foo.h.in</u> file:
<u>#cmakedefine FOO_ENABLE</u>
<u>#cmakedefine FOO_STRING "@FOO_STRING@"</u>

An adjacent CMakeLists.txt may use configure_file to configure the header:
<u>option(FOO_ENABLE "Enable Foo" ON)</u>
<u>if(FOO_ENABLE)</u>
  <u>set(FOO_STRING "foo")</u>
<u>endif()</u>

<u>configure_file(foo.h.in foo.h @ONLY)</u>
This creates a foo.h in the build directory corresponding to this source directory. If the FOO_ENABLE option is on, the configured file will contain:
<u>#define FOO_ENABLE</u>
<u>#define FOO_STRING "foo"</u>

## 10、set

**语法：** SET(VAR [VALUE] [CACHE TYPE DOCSTRING [FORCE]]) 
**指令功能:** 用来显式的定义变量 
**例子:** SET (SRC_LST main.c other.c) 
**说明:** 用变量代替值，例子中定义SRC_LST代替后面的字符串。

## 11、使用变量

${SRC}    // 变量SRC

## 12、ADD_DEFINITIONS

添加宏定义 

# 部分常用命令

| **INCLUDE_DIRECTORIES**( "dir1" "dir2" ... )                 | 头文件路径，相当于编译器参数 -Idir1 -Idir2                   |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| **LINK_DIRECTORIES**("dir1" "dir2")                          | 库文件路径。注意： 由于历史原因，相对路径会原样传递给链接器。 尽量使用FIND_LIBRARY而避免使用这个。 |
| **AUX_SOURCE_DIRECTORY**( “sourcedir” variable)              | 收集目录中的文件名并赋值给变量                               |
| **ADD_EXECUTABLE**                                           | 可执行程序目标                                               |
| **ADD_LIBRARY**                                              | 库目标                                                       |
| **ADD_CUSTOM_TARGET**                                        | 自定义目标                                                   |
| **ADD_DEPENDENCIES( target1 t2 t3 )**                        | 目标target1依赖于t2 t3                                       |
| **ADD_DEFINITIONS( "-Wall -ansi")**                          | 本意是供设置 -D... /D... 等编译预处理需要的宏定义参数，对比 REMOVE_DEFINITIONS() |
| **TARGET_LINK_LIBRARIES**( target-name lib1 lib2 ...)        | 设置单个目标需要链接的库                                     |
| **LINK_LIBRARIES**( lib1 lib2 ...)                           | 设置所有目标需要链接的库                                     |
| **SET_TARGET_PROPERTIES**( ... )                             | 设置目标的属性 OUTPUT_NAME, VERSION, ....                    |
| **MESSAGE**(...)                                             |                                                              |
| **INSTALL**( FILES “f1” “f2”DESTINATION . )                  | DESTINATION 相对于 ${CMAKE_INSTALL_PREFIX}                   |
| **SET**( VAR value [CACHE TYPE DOCSTRING [FORCE]])           |                                                              |
| **LIST**( APPEND\|INSERT\|LENGTH\|GET\| REMOVE_ITEM\|REMOVE_AT\|SORT ...) | 列表操作                                                     |
| **STRING**( TOUPPER\|TOLOWER\|LENGTH\| SUBSTRING\|REPLACE\|REGEX ...) | 字符串操作                                                   |
| **SEPARATE_ARGUMENTS**( VAR )                                | 转换空格分隔的字符串到列表                                   |
| **FILE**( WRITE\|READ\|APPEND\|GLOB\| GLOB_RECURSE\|REMOVE\|MAKE_DIRECTORY ...) | 文件操作                                                     |
| **FIND_FILE**                                                | 注意 CMAKE_INCLUDE_PATH                                      |
| **FIND_PATH**                                                | 注意 CMAKE_INCLUDE_PATH                                      |
| **FIND_LIBRARY**                                             | 注意 CMAKE_LIBRARY_PATH                                      |
| **FIND_PROGRAM**                                             |                                                              |
| **FIND_PACKAGE**                                             | 注意 CMAKE_MODULE_PATH                                       |
| **EXEC_PROGRAM**( bin [work_dir] ARGS <..> [OUTPUT_VARIABLE var] [RETURN_VALUE var] ) | 执行外部程序                                                 |
| **OPTION**( OPTION_VAR “description” [initial value] )       |                                                              |

## 编译Debug模式

cmake  .   -DCMAKE_BUILD_TYPE=Debug



## 编译Release模式

 cmake ../src -DCMAKE_BUILD_TYPE=Release





# vs2010 编译

\# 用于生成 Visual Studio 10Win64 工程文件

CMake -G "Visual Studio 10 Win64"

\# 用于生成 Visual Studio 10Win32 工程文件

CMake -G "Visual Studio 10"