## 源码解析

前面已有提到Etcd是由Go语言实现的，所以在阅读Etcd源码之前，首先需要搭建Go语言的开发环境。以下为环境搭建的详细步骤：

### 环境准备

#### Go语言安装
##### Windows安装：

 有两种安装方式，源码安装以及MSI安装，本文介绍以应用程序安装。
- 首先下载相应的安装包：https://redirector.gvt1.com/edgedl/go/go1.11.2.windows-amd64.msi
- 下载成功之后直接双击安装
- 设置环境变量
- 创建工作目录.   在User/Magic/go
- 将工作目录也添加到环境变量
   
##### Mac安装：
-  下载pkg包安装
https://redirector.gvt1.com/edgedl/go/go1.11.2.darwin-amd64.pkg
-  创建工作目录
>  mkdir -p /Users/magic/go

-  设置环境变量
> export GOPATH=/Users/magic/go  
> export GOBIN=`$`GOPATH/bin
> export PATH=`$`PATH:/Users/magic/go/bin 
    
    

    

##### Linux安装：
Linux下安装更加简单，设置环境变量的方式跟mac下基本一致。
- Linux下之后可以用yum install go(CentOS).  apt-get install go (Ubuntu)
- 设置环境变量
  
#### Git的安装：
   

- 关于Git的安装，直接访问:
https://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000

#### Docker的安装：

>    Docker的安装可以参考此：https://docs.docker.com/engine/installation/#supported-platforms

#### 编辑器：

本人喜欢用vscode写go, 当然编辑器的使用因人而异，适合自己的才是最好的。

---

#### 项目地址
- https://github.com/csunny/etcd-from-arch-to-souce-code

#### 参考文章:
 
 - Docker安装: https://docs.docker.com/engine/installation/#time-based-release-schedule 
 - Go安装:  https://golang.org/doc/install    
 - Git:https://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000
 - VScode: https://code.visualstudio.com/
 - Sublime:    https://www.sublimetext.com/