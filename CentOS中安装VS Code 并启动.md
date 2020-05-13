# [CentOS-7 中安装VS Code 并启动](https://www.cnblogs.com/-Fly/p/11101978.html)

 

## VSCode安装

安装平台：CentOS7

安装方法：

1。在官网上下载64位（或者32位）的rpm包（官网地址：https://code.visualstudio.com/Download）

2。在rpm包所在目录代开终端，执行以下命令：

**sudo rpm -ivh code-1.35.1-1560350390.el7.x86_64.rpm**

3。若提示缺少libXss.so,则需要安装libXScrnSaver相关的依赖，搜索文件并安装：

**sudo yum search libXScrnSaver**

**sudo yum install libXScrnSaver-devel.x86_64 libXScrnSaver.x86_64**

4。安装完成之后，重新执行第二步。

5。启动VS Code:

**/usr/share/code/code --user-data-dir**

如报以下错误：

**/usr/share/code/code: /lib64/libnss3.so: version `NSS_3.22' not found (required by /usr/share/code/code)**
**/usr/share/code/code: /lib64/libdbus-1.so.3: no version information available (required by /usr/share/code/code)**

则需要安装nss依赖，命名如下：

**sudo yun install nss**

6。完成之后，重新执行第五步。

7。启动成功