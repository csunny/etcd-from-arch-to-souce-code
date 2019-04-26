# 架构介绍

如下图所示，ETCD三节点集群简易架构图。 从图可以看出，ETCD中节点之间是通过对等网络的方式进行通信的。但是在不同的时期每个节点所扮演的角色不一样。
严格来说，ETCD节点有三种角色：
- Leader
- Flower
- Candidate
节点角色会在以上三种角色中进行切换。其中每个节点又主要有以下几个核心模块:
- 接口层
- Raft协议
    - 选主
    - wal日志
    - snap快照
  
- 复制状态机
- 持久存储K-V数据库
  
当然以上也仅仅是粗略的划分, 但也能大概说明问题。 这里我们结合上述架构图来解释各个模块的功能，以及一个完整的ETCD集群的工作流程。


![](https://raw.githubusercontent.com/csunny/etcd-from-arch-to-souce-code/master/_asserts/images/etcd_arch.jpg)

下面是一个更为细致的划分，通过分层的方式，将etcd划分为4层，依次为表现层、网络层、应用层、数据层。

#### 表现层
主要包含了命令行工具，以及restful的api。客户端可以通过命令行或者是restful api的方式与etcd集群进行通信。

#### 网络层
主要包含代理和SDK，ETCD提供了三种协议的通信方式，分别为HTTP、TCP、gRPC。

#### 应用层
应用层包含了Raft协议、复制状态机、多版本并发控、Watch、K-V数据存储、分布式事务等核心功能。

#### 数据层
数据层有两部分，一部分为内存数据，一部分是磁盘数据。 其中内存中维护的数据主要是Key与revision之间的B-tree索引。
磁盘里面存储的文件有三部分，一部分就是核心的数据文件，在snap下面的db文件中保存，还有就是raft协议依赖的wal日志文件
和snap快照文件。

![](https://raw.githubusercontent.com/csunny/etcd-from-arch-to-souce-code/master/_asserts/images/arch_design.jpg)
