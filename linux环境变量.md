# linux环境变量

# 属性区别（转载http://www.cnblogs.com/fuxueming/p/6603119.html）

**1./ etc / bashrc：**
 为每一个运行bash shell的用户执行此文件，当bash shell被打开时，该文件被读取。也就是说，当用户shell执行了bash时，运  行这个文件。

**2.〜/ .bashrc** 

该文件存储的是专属于个人bash shell的信息，当登录时以及每次打开一个新的shell时，执行这个文件。在这个文件里可以自定义用户专属的个人信息。

**3.~/.bash_profile**

每个用户都可使用该文件输入专用于自己使用的shell信息,当用户登录时,该 文件仅仅执行一次!默认情况下,他设置一些环境变量,执行用户的.bashrc文件.

**4./etc/profile**

此文件为系统的每个用户设置环境信息,当用户第一次登录时,该文件被执行. 并从/etc/profile.d目录的配置文件中搜集shell的设置。

**5、/etc/environment**

系统的环境变量，系统应用程序的执行与用户环境可以是无关的，但与系统环境是相关的

 

1、在登录时,操作系统定制用户环境时使用的第一个文件就是 /etc/profile ,此文件为系统的每个用户设置环境信息,当用户第一次登录时,该文件被执行。
2、在登录时操作系统使用的第二个文件是 /etc/environment  ，系统在读取你自己的profile 前,设置环境文件的环境变量。
3、在登录时用到的第三个文件是.profile文件,每个用户都可使用该文件输入专用于自己使用的shell信息,,该 文件仅仅执行一次!默认情况下,他设置一些环境变量,执行用户的.bashrc文件。/etc/bashrc:为每一个运行bash shell的用户执行此文件。当bash shell 被打开时,该文件被读取。

4、 /etc/environment是设置整个系统的环境，而/etc/profile是设置所有用户的环境，前者与登录用户无关，后者与登录用户有关。

先执行/etc/enviroment，后执行/etc/profile

# 使用区别([转载http://andy136566.iteye.com/blog/1025338](http://andy136566.iteye.com/blog/1025338))

如果是root用户运行java程序，直接在/etc/profile里设置java的环境变量;
如果是其他用户运行java程序，可编辑宿主目录的.bashrc文件，加入相关java的环境变量。

 

先将export LANG=zh_CN加入/etc/profile ,退出系统重新登录，登录提示显示英文。将/etc/profile 中的export LANG=zh_CN删除，将LNAG=zh_CN加入/etc/environment，退出系统重新登录，登录提示显示中文。用户环境建立的过程中总是先执行/etc/profile然后在读取/etc/environment。为什么会有如上所叙的不同呢?

​    应该是先执行/etc/environment，后执行/etc/profile。
​    /etc/environment是设置整个系统的环境，而/etc/profile是设置所有用户的环境，前者与登录用户无关，后者与登录用户有关。
​    系统应用程序的执行与用户环境可以是无关的，但与系统环境是相关的，所以当你登录时，你看到的提示信息，象日期、时间信息的显示格式与系统环境的LANG是相关的，缺省LANG=en_US，如果系统环境LANG=zh_CN，则提示信息是中文的，否则是英文的。

 

 

对于用户的SHELL初始化而言是先执行/etc/profile,再读取文件/etc/environment.对整个系统而言是先执行/etc/environment。这样理解正确吗?
    /etc/enviroment --> /etc/profile --> $HOME/.profile  -->$HOME/.env (如果存在)


    /etc/profile 是所有用户的环境变量
    /etc/enviroment是系统的环境变量
    登陆系统时shell读取的顺序应该是
       /etc/profile ->/etc/enviroment -->$HOME/.profile  -->$HOME/.env
    原因应该是jtw所说的用户环境和系统环境的区别了