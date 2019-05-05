## 
## 前言

  在第一节中，对IPFS下了很多定义，在第二节中又引入了很多概念。 对于一个技术人员来说，前面两节无疑是枯燥的。那么接下来，开始熟悉的节奏，开发环境搭建。

---

## 编辑器

   打出编辑器这三个字的时候，不自觉地，我打了个激灵(😓)。在程序员这个圈子里，对于编辑器的选择，就好像说“PHP是世界上最好的语言”一样。是个梗，而且一直争论不休，从未有谁能够完胜别人。 当然，我这里提编辑器，并不想争论各个编辑器的优劣。我只是介绍几种选择方案，以及我自己的开发环境。 

  由于在本系列文章里面，主要是围绕IPFS的Go语言相关的源码。一方面是因为Go语言的实现更全，代码完成度更高。此外也有我自己作为技术人员的一点小偏执。所以以下编辑器主要围绕Go语言来展开。

**Goland** 

JetBrains，想必这个名字在程序员的圈子里，绝大多数人都听过，或者正在使用他们的产品。是的，goland就是大名鼎鼎的JetBrains出品的一款针对Go语言的编辑器。可以说简单、无脑容易上手，同时也很好用。也支持一些常见的快捷键以及自定义环境，可以说是一款相当不错的编辑器。

嗯，当然有缺点，那就是慢！此外，JetBrains出品的产品都是高度语言定制化。Python有pycharm，java有idea，前端有webstorm。作为一个经常需要同时写几门开发语言的同学来说，相当受罪。 之前我也有过一段时间与编辑器的斗争，最后还是毅然而然的抛弃了JetBrains 全家桶。

**VIM**

毫无疑问，VIM确实非常强大。 我这里说VIM打开文件的速度超越任何编辑器，相信大家没意见吧？ 同时VIM也是最轻量的编辑工具，同时也不限开发语言。 

尽管VIM有这么多优点，但是其缺点也相当明显，VIM本身没有带任何的语法提示、语法校验、格式化等等人性化的功能。 需要配置插件。 所以在VIM使用过程中，要维护一个相当长的配置文件，从插件到快捷键。如果对VIM熟悉的同学来说，使用起来确实相当快捷，但是对对于那些初学者，或者对VIM不够熟悉的同学来说，以VIM为日常开发环境反而影响开发效率。 

但，我知道，很多人不愿意舍弃VIM，尤其是在unix环境下开发的同学。 

**VSCode**

在遇到Vscode之前，其实我觉得大多数编辑器都没啥区别。直到开始使用Vscode，慢慢变成vscode忠实用户。 我才知道，原来天下编辑器共分两类：一类是Vscode，一类是其他。

请原谅我对Vscode的推崇，因为它确实好用。

**打造VIM+Vscode+Go语言的开发环境**

Vscode的安装

- Mac安装

    mac下安装vscode相当简单，在官网下载一个vscode dmg然后安装就ok。[官网地址](https://code.visualstudio.com/)

- Windows下安装

    跟mac下一样，下载对应的exe文件，然后安装即可。

- Linux下安装

    俗话说的好，你都使用Linux了，安装软件的事情，肯定相当熟悉。

Go语言安装

 Go语言的安装这里就不仔细讲了，网上一大堆文章。另外在我的另一个专栏里面有一篇 [《Go语言环境搭建》](https://xiaozhuanlan.com/topic/8930542671) 如果对Go语言安装有问题的同学也可以看看。

VsCode配置

VsCode上手非常容易，其实不需要做任何配置都可以玩的很溜。当然，为了进一步提高开发效率，所以还是可以做一些必要的配置。 

**插件安装**
安装完成打开vscode， 点击左侧栏目的红色序号标注的1，然后在搜索框搜索Go，然后第一个就是Vscode的go语言插件，如果未安装，右侧序号2会是Install，点击安装即可。序号3区域是对此插件的介绍，以及其默认的一些配置和快捷键。

除了Go插件，开发Go语言还需要以下插件

- Go  
- Code Runner  快捷运行Go代码  常见的快捷键是command+R（mac）windows是（ctrl+R）
- Vim  在vscode里面使用vim编辑模式
- VSCode Icons 根据文件名称显示图标
- Path Intellisense 自动补全文件路径
- TODO Highlight 高亮TODO

必要的插件就这几个吧，其他的插件，按照自己的需求选择性安装即可。

![](https://diycode.b0.upaiyun.com/photo/2018/e03b4c4e69771bc2c82a7767c6278d3b.png)
**快捷键设置**
在VSCode中快捷键的设置相当重要。 查寻快捷键的命令command+shift+p, 修改快捷键command+k,command+s 然后调出修改快捷键的文件，根据自己喜好修改即可。

常见的快捷键
打开新窗口 command+T  
打开文件夹 command+O
新建文件 command + N
关闭文件 command + W
分屏 command+D   command+shift+D
还有一些其他快捷键，自己可以摸索使用。这里就不一一列举啦。

**IPFS代码下载**
这里我们主要剖析go-ipfs代码
如果之前安装了Go语言，直接使用go get进行下载

```
// 下载代码
go get -u -d github.com/ipfs/go-ipfs 
// 安装
cd $GOPATH/src/github.com/ipfs/go-ipfs
make install

```

这样IPFS的源码下载、安装就成功了。由于在IPFS中，代码的依赖管理是采用的gx，而不是目前使用官方的dep，所以对于之前使用dep管理依赖的同学，要调整下。 安装go-ipfs依赖包
```
go get -u github.com/whyrusleeping/gx
```

到这里，整个开发环境就准备的差不多了，接下来我们来运行一个简单的命令，并打个断点，debug个一把，作为本章内容的终结。

在debug之前，需要安装一个go语言的库。
```
go get github.com/derekparker/delv
```

Debug lanch 配置文件
```
{
    // Use IntelliSense to learn about possible attributes.
    // Hover to view descriptions of existing attributes.
    // For more information, visit: https://go.microsoft.com/fwlink/?linkid=830387
    "version": "0.2.0",
    "configurations": [
        {
            "name": "Launch",
            "type": "go",
            "request": "launch",
            "mode": "auto",
            "remotePath": "",
            "port": 2345,
            "host": "127.0.0.1",
            "program": "${file}",     // workspaceRoot 代表当前打开文件的跟目录
            "env": {
                "GOPATH": "/Users/magic/go"
            },
            "args": ["ls", "QmfEE1CwpwfJcj54AAhz16HU3VkeUkP41Ta953Y1Evi3qb", "--resolve-type"],
            "showLog": true
        }
    ]
}

```

执行F5 运行debug显示如下, 由此说明我们开发环境搭建ok，可以正常运行IPFS代码，进行debug。
![](https://diycode.b0.upaiyun.com/photo/2018/1bc2832fd30b6fcb03be89eb9a5d5e91.png)

以上，我们就搭建好了go-ipfs的开发环境。 后面我们会在这个环境中进行代码的调试与源码分析。


## 参考
- [gx依赖管理](https://github.com/whyrusleeping/gx)




