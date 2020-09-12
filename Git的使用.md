# Git的使用

## 一、Git工作区域

**1、Git Repository(Git 仓库) ** 

最终确定的文件保存到仓库，成为一个新的版本，并且对他人可见 

**2、暂存区**

暂存已经修改的文件最后统一提交到git仓库中

**3、工作区（Working Directory）**

添加、编辑、修改文件等动作



## 二、向仓库中添加文件流程

**1、git status**

查看文件状态

**2、git add .**

将当前文件存入***暂存区***

**3、git commit -m "描述"**

将文件人提交到***仓库***

**4、git rm '文件名'**

从git中删除文件，然后提交就能生效

## 三、Git基础设置

Git安装完成之后，需要时行一些基本信息设置 

**1、设置用户名**

git config --global user.name  'w1146869587'

**2、设置用户邮箱**

git config --global user.email 'wah1146869587@126.com'

**3、查看设置**

git config --list 

**提示:** 用户名在GitHub上是唯一的

## 四、远程仓库

**1、使用远程仓库的目的**

作用：备份，实现代码共享集中化管理



![image-20200321213806482](image-20200321213806482.png)

**2、将本地仓库推送到远程仓库**

git push 命令

![image-20200321213852139](image-20200321213852139.png)



**注意事项：**

vi ./git/config 当前仓库的配置

**3、更新本地仓库**

git pull

## 设置代理

如果要设置全局代理，可以依照这样设置

```text
git config --global http.proxy http://127.0.0.1:1080
git config --global https.proxy https://127.0.0.1:1080



git config --global --unset http.proxy
git config --global --unset https.proxy


git config --global http.postBuffer 524288000
这是个很有效的配置，修改后速度有质的提升
```

