## 表现层

在ETCD的整个架构中，我将ECTD分为了四层。分别为表现层、网络层、应用层和数据层。表现层这里主要指的是命令行以及restful的api。 也就是我们可以通过etcd提供的命令行工具，或者是restful api与etcd整个集群进行交互。

由于etcd同时兼容v2、v3两个版本，所以命令行工具也同时有v2和v3, 可以使用如下命令进行切换
```
export ETCDCTL_API=2    # 切换到v2版本
export ETCDCTL_API=3    # 切换到v3版本
```

在使用之前，也可以通过命令来查看当前的命令行是那个版本的。 直接在终端运行命令 `etcdctl` 即可查看

v2版本

![](\_asserts\images\etcdctl_v2.jpg)

v3版本

![](\_asserts\images\etcdctl_3.jpg)