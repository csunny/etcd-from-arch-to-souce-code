## 共识算法

在上一节我们提到了，为了多节点中多副本数据的一致性，提出来一致性协议，而针对一致性协议又衍生出了很多的一致性算法。
简单来讲，共识算法又可以分为下面几部分:
- 开放网络
    - 区块链公链
        - pow (proof of power)
        - pos (proof of stake)
        - dpos (Delegated proof of stake)
        - ripple
    - 区块链联盟链
        - pbft (Practical Byzantine Fault Tolerance）)
        - dbft(Delegated Byzantine Fault Tolerant))
- 内部网络
    - 分布式一致性系统
        - paxos
        - raft  

![](https://raw.githubusercontent.com/csunny/etcd-from-arch-to-souce-code/master/_asserts/images/consensus_algorithm.jpg)

当然在这里，我们不打算介绍区块链领域里面的那些共识算法，感兴趣的同学，可以访问我的[github](https://github.com/csunny)来查看，在里面我有解释，
以及具体的代码实现。本书中，我们只介绍raft共识算法。