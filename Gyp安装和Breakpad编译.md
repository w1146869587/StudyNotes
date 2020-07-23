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
gyp.bat  -–no-circular-check “../../client/windows/breakpad_client.gyp”

三、查看支持的选项

gyp_main.py --help

四、注意

一定不能使用绝对路径，要使用相对路径，所以为什么要拷贝gyp文件夹到tools文件夹下面。 



五、提示了 Unitests报错

$ gyp.bat --no-circular-check "../../client/windows/breakpad_client.gyp"
Warning: Missing input files:
..\..\client\windows\unittests\..\..\..\testing\src\gmock-all.cc
..\..\client\windows\unittests\..\..\..\testing\gtest\src\gtest-all.cc
..\..\client\windows\unittests\..\..\..\testing\src\gmock_main.cc

提示，missing几个文件，所以我们这里不能编译unittest下的两个工程，暂时不理会 

错误： 
2>C:\Program Files (x86)\Windows Kits\8.1\Include\um\dbghelp.h(1544): error C2220: 警告被视为错误 - 没有生成“object”文件 
2>C:\Program Files (x86)\Windows Kits\8.1\Include\um\dbghelp.h(1544): warning C4091: “typedef ”: 没有声明变量时忽略“”的左侧 
2>C:\Program Files (x86)\Windows Kits\8.1\Include\um\dbghelp.h(3190): warning C4091: “typedef ”: 没有声明变量时忽略“”的左侧 
4>C:\Program Files (x86)\Windows Kits\8.1\Include\um\dbghelp.h(1544): error C2220: 警告被视为错误 - 没有生成“object”文件 
4>C:\Program Files (x86)\Windows Kits\8.1\Include\um\dbghelp.h(1544): warning C4091: “typedef ”: 没有声明变量时忽略“”的左侧 
4>C:\Program Files (x86)\Windows Kits\8.1\Include\um\dbghelp.h(3190): warning C4091: “typedef ”: 没有声明变量时忽略“”的左侧

解决方案，把警告当错误 选择否。

# 使用Breakpad生成dump文件 

前戏有点复杂，现在开始使用。把之前生成的几个lib，包含进来 
common.lib 
exception_handler.lib 
crash_generation_server.lib 
crash_generation_client.lib

头文件目录导进来： 


编写代码：

#include <cstdio>  
#include "client/windows/handler/exception_handler.h"  

namespace {

  static bool callback(const wchar_t *dump_path, const wchar_t *id,
    void *context, EXCEPTION_POINTERS *exinfo,
    MDRawAssertionInfo *assertion,
    bool succeeded) {
    if (succeeded) {
      printf("dump guid is %ws\n", id);
    }
    else {
      printf("dump failed\n");
    }
    fflush(stdout);

    return succeeded;
  }

  static void CrashFunction() {
    int *i = reinterpret_cast<int*>(0x45);
    *i = 5;  // crash!  
  }

}  // namespace  

int main(int argc, char **argv) {
  google_breakpad::ExceptionHandler eh(
    L".", NULL, callback, NULL,
    google_breakpad::ExceptionHandler::HANDLER_ALL);
  CrashFunction();
  printf("did not crash?\n");
  return 0;
}
 
 
可能的错误： 
common.lib(guid_string.obj) : error LNK2038: 检测到“RuntimeLibrary”的不匹配项: 值“MTd_StaticDebug”不匹配值“MDd_DynamicDebug”(main.obj 中)

解决方法： 
就是编译库的时候 和现在使用库的工程 选择的代码生成方式不一致： 


如何根据生成的dump定位错误代码 
文件->打开->文件，找到刚生成的dump文件，然后点击“使用仅限本机进行调试” 


结果： 

准确定位！！！！