## 网络层

在前面的介绍中，我们不仅介绍了ISO OSI七层网络模型，还介绍了传输层的TCP/UDP协议，以及应用层的HTTP协议，以及RPC协议。 所以我们在etcd架构分层的过程中，单独分离出来一层网络层。

在etcd中，网络层几乎用到了我们前面提到的很多网络知识，包括tcp、rpc、http等等。所以，根据以上知识点，我这里将
proxy跟sdk这两部分划分到了网络层。

代理层又分为三种代理
Proxy
- httpproxy
- tcpproxy
- grpcproxy

etcd提供了两个版本的sdk

SDK
- clientv2
- clientv3


接下来, 我们详细介绍下，每部分的内容。
