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

