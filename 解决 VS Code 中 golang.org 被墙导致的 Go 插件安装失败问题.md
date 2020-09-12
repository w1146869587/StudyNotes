# 解决 VS Code 中 golang.org 被墙导致的 Go 插件安装失败问题

[![img](https://upload.jianshu.io/users/upload_avatars/1900931/abc9387a175c.jpg?imageMogr2/auto-orient/strip|imageView2/1/w/96/h/96/format/webp)](https://www.jianshu.com/u/641c6eff24ec)

[苏易北](https://www.jianshu.com/u/641c6eff24ec)关注

22018.12.28 22:38:23字数 623阅读 25,683

> **Google** 在今年一月发布了 [golang.org](https://golang.org/) 的镜像站 [golang.google.cn](https://golang.google.cn/)，中国大陆可直接访问。详情参见 [Hello, 中国! | The Go Blog](https://blog.golang.org/hello-china)
> 欢迎点击查看我的[博客原文](https://abelsu7.top/2018/12/28/go-vscode-plugin/)

![img](https://upload-images.jianshu.io/upload_images/1900931-f4783529befa5c14.png?imageMogr2/auto-orient/strip|imageView2/2/w/600/format/webp)

**微软官方**开发的 [Go for Visual Studio Code](https://marketplace.visualstudio.com/items?itemName=ms-vscode.Go) 插件为 [Go 语言](https://golang.google.cn/) 提供了丰富的支持。在 [VS Code](https://code.visualstudio.com/) 中首次打开 Go 工作区后，VS Code 会自动检测当前开发环境为 Go 并推荐安装上述插件。

然而 Go 插件的安装并不顺利：输出窗口的安装信息提示其中一些依赖工具安装失败：



```bash
Installing github.com/mdempsky/gocode FAILED
Installing github.com/ramya-rao-a/go-outline FAILED
Installing github.com/acroca/go-symbols FAILED
Installing golang.org/x/tools/cmd/guru FAILED
Installing golang.org/x/tools/cmd/gorename FAILED
Installing github.com/stamblerre/gocode FAILED
Installing github.com/ianthehat/godef FAILED
Installing github.com/sqs/goreturns FAILED
Installing golang.org/x/lint/golint FAILED

9 tools failed to install.
```

手动使用`go get -v github.com/mdempsky/gocode`等命令同样提示网络连接失败。

### 失败原因

原因其实很简单：[golang.org](https://golang.org/) 在国内由于一些~~众所周知的~~原因**无法直接访问**，而`go get`在获取`gocode`、`go-def`、`golint`等插件依赖工具的源码时，需要从 [golang.org](https://golang.org/) 上拉取部分代码至`GOPATH`，自然就导致了最后这些依赖于 [golang.org](https://golang.org/) 代码的依赖工具安装失败。

### 解决办法

解决也并不复杂：先通过`git clone`命令手动将依赖工具的源码拉取至`GOPATH`的对应路径，再通过`go install`命令安装依赖工具。

以 **Windows** 为例，首先进入`%GOPATH%\src\`目录，并创建`golang.org\x`。

之后进入`%GOPATH%\src\golang.org\x`，使用下列命令下载插件依赖工具的源码：



```bash
git clone https://github.com/golang/tools.git tools
```

`git clone`命令执行完毕后，所需的工具源码就都保存在`tools`目录中。

最后进入`%GOPATH%`目录，根据之前的安装失败提示信息安装对应的依赖工具：



```bash
go install github.com/mdempsky/gocode
go install github.com/ramya-rao-a/go-outline
go install github.com/acroca/go-symbols
go install golang.org/x/tools/cmd/guru
go install golang.org/x/tools/cmd/gorename
go install github.com/stamblerre/gocode
go install github.com/ianthehat/godef
go install github.com/sqs/goreturns
go install golang.org/x/lint/golint
```

### 安装 golint

在执行`go install`命令安装 **golint** 时，提示信息如下：



```bash
PS C:\Users\abel1\go> go install golang.org/x/lint/golint

can't load package: package golang.org/x/lint/golint: cannot find package "golang.org/x/lint/golint" in any of:
        C:\Go\src\golang.org\x\lint\golint (from $GOROOT)
        C:\Users\abel1\go\src\golang.org\x\lint\golint (from $GOPATH)
```

这是因为 **golint 的源码在**`lint`**下，而不是**`tools`，需要单独拉取 golint 源码。

进入`%GOPATH%\src\golang.org\x`，执行下列命令拉取 golint 源码：



```bash
git clone https://github.com/golang/lint
```

最后回到`%GOPATH%`，通过`go install`安装 golint：



```bash
go install github.com/golang/x/lint/golint
```

**重启 VS Code** 后，插件就可以正常使用了。**Let's go for Go！**

> **参考文章**
>
> 1. [解决 VS Code 中 golang.org 被墙导致的 Go 插件安装失败问题 | 苏易北](https://mp.weixin.qq.com/s/hjE5Uxppif4pdlRSKEr7HA)
> 2. [解决vscode中golang插件依赖安装失败问题 | 简书](https://www.jianshu.com/p/6293503522bc)
> 3. [VSCode安装go语言开发环境，go插件问题解决 | CSDN](https://blog.csdn.net/yo_oygo/article/details/79065966)



21人点赞



[Go](https://www.jianshu.com/nb/32805949)