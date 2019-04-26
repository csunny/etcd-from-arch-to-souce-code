## 分布式系统模型

从分布式系统角色的角度来说，我们可以简单的将分布式系统分为对等和非对等分布式系统。而进一步我们又可以将其划分为以下三种模型：

一、 C/S模型

![](https://github.com/csunny/etcd-from-arch-to-souce-code/tree/master/_asserts/images/c_s.jpg?row=true)

当前占据主导地位的是非对称分布式系统，也就是系统之间不同的服务之间承担着不同的角色。
典型的就是C/S架构模型: 客户端发送请求到服务器，服务接收请求进行响应。

二、 Peer-to-Peer模型

![](https://github.com/csunny/etcd-from-arch-to-souce-code/tree/master/_asserts/images\peer-to-peer.jpg?row=true)

如果在整个过程中，两个服务的角色是对等的，两者都可以接受请求，并对消息做出响应。典型的就是点对点分布式系统。 对于点对点的分布式系统，当下使用
最广泛，也是最火热的要属于区块链技术。

三、Filter模型

![](https://github.com/csunny/etcd-from-arch-to-souce-code/tree/master/_asserts/images\filter.jpg?row=true)

类似于中间件，一个服务发送消息给到另一个中间服务，中间服务在将消息发送给第三方服务的时候会进行处理，这也是一种非常普遍的模型。


当然，在一个分布式系统当中，随着系统的演变发展，一个系统当中往往都是以上三种模型以共存的方式协作。ETCD也不例外，在ETCD中虽然以Peer-to-Peer为主要
的角色，但C/S跟Filter也是其中不可或缺的配角。
